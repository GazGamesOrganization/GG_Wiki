# Nome do Projeto

  
`Descrição breve do projeto ex:`
VersionOverlay é uma ferramenta para sobrepor informações de versão em seus projetos. Com ela, você pode facilmente exibir a versão atual do seu projeto em um local visível, facilitando o rastreamento e a identificação da versão em uso.

  

## Como Usar o Projeto

`Guia de como instalar o projeto`
Ex:
1. Adicione o VersionOverlay ao seu projeto. [GGTools Guia de Instalação]

  

2. Adicione o componente VersionOverlay a um GameObject na cena onde deseja exibir a versão.

  

## Configurações

`Guia de Configurações do projeto`
  Ex:

`onlyInDevelopmentBuild`: Se verdadeiro, a sobreposição de versão só será exibida em builds de desenvolvimento.

  

`margin`: Define a margem ao redor da sobreposição de versão.

`position`: Define a posição da sobreposição de versão na tela. As opções incluem:

  

- TopLeft

- TopRight

- BottomLeft

- BottomRight

  

`fontSize`: Define o tamanho da fonte usada para exibir a versão.

  

`color`: Define a cor do texto da versão.

  
  ### Use o blockquote '>' para responder possíveis duvidas do código
  
  EX:
  
`dontDestroyOnLoad`: Se verdadeiro, o GameObject com o VersionOverlay não será destruído ao carregar novas cenas.

> Caso você tenha 2 na mesma cena, o sistema irá destruir o mais novo para evitar duplicações.

  

```cs

  

void Awake()

{

    var other = FindAnyObjectByType<VersionOverlay>();

  

    if (other != null && other != this)

    {

        Destroy(gameObject);

        return;

    }

    if (dontDestroyOnLoad)

    {

        DontDestroyOnLoad(gameObject);

    }

}

```

  

`textSize`: Define o tamanho da caixa de texto usada para exibir a versão.

  

## Features

  
`Guia sobre as Features o projeto`
	Ex:

`OnGUI`: Evento que é chamado para desenhar a interface gráfica da sobreposição de versão. Usando o `Application.version` para obter a versão atual do projeto e exibi-la na tela.

  

```cs

  

void OnGUI()

{

    if (onlyInDevelopmentBuild && !Debug.isDebugBuild) return;

  

    string txt = $"v{Application.version}";

  

    var style = new GUIStyle(GUI.skin.label);

    style.fontSize = fontSize;

    style.normal.textColor = color;

  

    switch (position)

    {

        default:

        case VersionOverlayPosition.TopLeft:

            style.alignment = TextAnchor.UpperLeft;

            break;

  

        case VersionOverlayPosition.TopRight:

            style.alignment = TextAnchor.UpperRight;

            break;

  

        case VersionOverlayPosition.BottomLeft:

            style.alignment = TextAnchor.LowerLeft;

            break;

  

        case VersionOverlayPosition.BottomRight:

            style.alignment = TextAnchor.LowerRight;

            break;

    }

    Rect rect = GetRect(position, margin, textSize.x, textSize.y);

    GUI.Label(new Rect(rect), txt, style);

}

  

```

  

`GetRect`: Método auxiliar para calcular a posição da caixa de texto com base na posição selecionada e na margem.

  

```cs

Rect GetRect(VersionOverlayPosition pos, Vector2 margin, float width, float height)

{

    switch (pos)

    {

        case VersionOverlayPosition.TopRight:

            return new Rect(

                Screen.width - width - margin.x,

                margin.y,

                width,

                height

            );

  

        case VersionOverlayPosition.BottomLeft:

            return new Rect(

                margin.x,

                Screen.height - height - margin.y,

                width,

                height

            );

  

        case VersionOverlayPosition.BottomRight:

            return new Rect(

                Screen.width - width - margin.x,

                Screen.height - height - margin.y,

                width,

                height

            );

  

        default: // TopLeft

            return new Rect(

                margin.x,

                margin.y,

                width,

                height

            );

    }

}

  

```

  

`VersionOverlayPosition`: Enum para definir as posições disponíveis para a sobreposição de versão.

  

```cs

public enum VersionOverlayPosition

{

    TopLeft,

    TopRight,

    BottomLeft,

    BottomRight

}

```