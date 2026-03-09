# TextInputDialog

TextInputDialog é uma ferramenta para exibir uma caixa de diálogo de entrada de texto personalizada. Com ela, você pode solicitar ao usuário que insira informações, como um nome, uma descrição ou qualquer outro tipo de texto, e processar essa entrada conforme necessário.

## Como Usar o TextInputDialog

`Guia de como instalar o projeto`
Ex:

1. Adicione o GGTools.BuildTools ao seu projeto. [GGTools Guia de Instalação]

2. Chame a função `TextInputDialog.Show` passando os parâmetros necessários para exibir a caixa de diálogo de entrada de texto.

## Features

`Show`: Método estático para exibir a caixa de diálogo de entrada de texto. Ele recebe um título, um texto padrão e uma ação de callback retornando uma string que será chamada quando o usuário confirmar a entrada.

```cs

public static void Show(string title, string defaultText, System.Action<string> callback)
{
    var window = CreateInstance<TextInputDialog>();
    window.titleContent = new GUIContent(title);
    window.text = defaultText;
    window.onConfirm = callback;
    window.position = new Rect(0, 0, Screen.width, Screen.height);
    window.ShowModal();
}



```

`OnGUI`: Evento que é chamado para desenhar a interface gráfica da caixa de diálogo. Ele exibe um campo de texto para o usuário inserir a informação e um botão de confirmação para processar a entrada.

```cs

void OnGUI()
{
    GUILayout.Label("Enter value:", EditorStyles.label);
    float halfHeight = 3 * position.height / 4f;

    text = EditorGUILayout.TextArea(text, GUILayout.Height(halfHeight));

    GUILayout.Space(10);

    GUILayout.BeginHorizontal();

    if (GUILayout.Button("Cancel"))
    {
        Close();
    }

    GUI.enabled = text.Length >= 100;

    if (GUILayout.Button("OK"))
    {
        onConfirm?.Invoke(text);
        Close();
    }

    GUI.enabled = true;

    GUILayout.EndHorizontal();
}



```

### Lucas Galo - 2026-03-06
