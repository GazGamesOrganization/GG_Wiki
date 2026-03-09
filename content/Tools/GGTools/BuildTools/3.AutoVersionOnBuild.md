# AutoVersionOnBuild

AutoVersionOnBuild é uma ferramenta que renomeia a pasta de build do seu projeto e _caso queira o nome do projeto também_ para incluir a versão atual do projeto usando o padrão de nomeclatura (**yyyyMMdd_HHmm_NomeDoProjeto**) . Logo depois ele pede para deixar um _PatchNotes_ no campo de texto para que seja criado um arquivo de texto dentro da pasta de build com o nome `patchNotes.txt`, contendo as informações. Isso facilita a identificação da versão da build apenas olhando para o nome da pasta e saber oque foi feito nela.

## Como Usar o AutoVersionOnBuild

1. Adicione o GGTools.BuildTools ao seu projeto. [GGTools Guia de Instalação]

2. No momento de selecionar a pasta de build crie uma nova pasta e selecione ela, o sistema irá renomear a pasta para o padrão de nomeclatura mencionado acima.

![Exemplo de seleção da pasta de build](PrintBuild.png)

## Configurações

`Caixa de pergunta Change Product Name`: Ela é criada HardCode então para trocar o titulo ou oque é escrito tem que ir na parte do codigo onde tem a função `EditorUtility.DisplayDialog` e trocar os parametros dela, o primeiro é o titulo da caixa de pergunta, o segundo é a mensagem, o terceiro é o texto do botão de confirmação e o quarto é o texto do botão de cancelamento, caso queira retirar o botão de cancelamento basta deixar ele como string vazia `""`.
`(string title, string message, string ok, string cancel = "")`

```cs
changeProductName = !EditorUtility.DisplayDialog(
"GGTools - Change Product Name",
$"Plataform: {report.summary.platform}\n" +
$"Do you want to keep the Product Name before starting the build?",
"Yes",
"No"
);
```

`Caixa de PatchNotes`: Ela é criada HardCode então para trocar o titulo ou oque é escrito tem que ir na parte do codigo onde tem a função `TextInputDialog.Show` e trocar os parametros dela, o primeiro é o titulo da caixa de pergunta, o segundo é a mensagem padrão, o terceiro é uma Action que retorna uma string para tocar assim que ele der OK (string title, string defaultText, System.Action<string> callback)

```cs
TextInputDialog.Show("Would you kindly leave a Patch Notes for this build?", "100 characters", (value) =>
{
     patchNotes = value;
     var buildPath = report.summary.outputPath;

     var buildFolder = Path.GetDirectoryName(buildPath);

     File.WriteAllText(Path.Combine(buildFolder, "patchNotes.txt"), patchNotes);

});
```

## Features

` OnPreprocessBuild`: Evento que toca antes de começar a buildar o projeto. Nele tem a função de pegar a data e hora atual para usar como versão do projeto, trocar o nome do produto caso o usuário queira e criar o arquivo de PatchNotes dentro da pasta de build.

```cs
public void OnPreprocessBuild(BuildReport report)
{
     bool current = EditorPrefs.GetBool(PrefKey, false);

     changeProductName = !EditorUtility.DisplayDialog(
          "GGTools - Change Product Name",
          $"Plataform: {report.summary.platform}\n" +
          $"Do you want to keep the Product Name before starting the build?",
          "Yes",
          "No"
     );
     TextInputDialog.Show("Would you kindly leave a Patch Notes for this build?", "100 characters", (value) =>
     {
          patchNotes = value;
          var buildPath = report.summary.outputPath;

          var buildFolder = Path.GetDirectoryName(buildPath);

          File.WriteAllText(Path.Combine(buildFolder, "patchNotes.txt"), patchNotes);

     });



     version = DateTime.Now.ToString("yyyyMMdd_HHmm");
     PlayerSettings.bundleVersion = version;
     if (changeProductName)
     {
          PlayerSettings.productName = $"{version}_{PlayerSettings.productName}";
     }
     PlayerSettings.companyName = "Gaz Games";
}
```

`OnPostprocessBuild`: Evento que toca depois de terminar de buildar o projeto. Nele tem a função de renomear a pasta de build para o padrão de nomeclatura mencionado acima e retorna o nome do projeto para a versão sem o versionamento.

```cs
public void OnPostprocessBuild(BuildReport report)
{


     var buildPath = report.summary.outputPath;

     var buildFolder = Path.GetDirectoryName(buildPath);

     var parent = Directory.GetParent(buildFolder).FullName;

     string projectName = GetBaseProjectName();

     string newFolder =
          Path.Combine(parent, $"{version}_{projectName}");

     if (!Directory.Exists(newFolder))
     {
          Directory.Move(buildFolder, newFolder);
     }


     PlayerSettings.productName = GetBaseProjectName();

}


```

`GetBaseProjectName`: Função para obter o nome base do projeto sem o versionamento.

```cs

public enum VersionOverlayPosition

{

static string GetBaseProjectName()
{
     string currentName = PlayerSettings.productName;

     if (System.Text.RegularExpressions.Regex.IsMatch(
          currentName,
          @"^\d{8}_\d{4}_"))
     {
          return currentName.Substring(14);
     }

     return currentName;
}

}

```

### Lucas Galo - 2026-03-06
