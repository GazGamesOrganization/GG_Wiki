Singleton responsável por gerenciar todas as informações necessárias para um percurso.

## Configs
Variáveis settadas pelo arquivo de configuração, gerenciado pelo [[Config Loader]], usadas para facilitar no ajuste de parâmetros do sistema
### Angle
Define as configurações de inclinação do percurso
`ANGLE_MIN`
`ANGLE_MAX`
`ANGLE_INCREMENT` - O quanto é adicionado ou reduzido do valor de ângulo ao clicar nos botões da interface
`ANGLE_CHANGE_RATE` - Quanto tempo ele demora para chegar no valor final
`ANGLE_SYMBOL` - Qual símbolo será mostrado na Interface
> Existem alguns lugares específicos em que esse símbolo é *Hardcoded* devido a demandas de clientes

### Power
Define as configurações de potência
`POWER_MIN`
`POWER_MAX`
`POWER_INCREMENT` - O quanto é adicionado ou reduzido do valor de power ao clicar nos botões da interface
`POWER_CHANGE_RATE` - Quanto tempo ele demora para chegar no valor final
`POWER_SYMBOL` - Qual símbolo será mostrado na Interface
> Existem alguns lugares específicos em que esse símbolo é *Hardcoded* devido a demandas de clientes

### Speed
Define as configurações de velocidade ou RPM (rotações por minuto)
`SPEED_MIN`
`SPEED_MAX`
`SPEED_INCREMENT` - O quanto é adicionado ou reduzido do valor de velocidade ao clicar nos botões da interface
`SPEED_CHANGE_RATE` - Quanto tempo ele demora para chegar no valor final
`SPEED_SYMBOL` - Qual símbolo será mostrado na Interface
> RPM ou Km/h

> Existem alguns lugares específicos em que esse símbolo é *Hardcoded* devido a demandas de clientes

### Curve
Define as configurações de curva do percurso
`CURVEMODE_MIN` - Menor número das divisões de curva para a interpolação do valor de `curveCurrent`
`CURVEMODE_MAX` - Maior número das divisões de curva para a interpolação do valor de `curveCurrent`
`CURVEMODE_INCREMENT` - O quanto é adicionado ou reduzido do valor de modo de curva ao clicar nos botões da interface

> O valor de `curveCurrent` é calculado a partir do valor de `curveMode`.
> `curveMode` define a posição atual dentro do intervalo de interpolação (`CURVE_MIN`, `CURVE_MAX`), em que a quantidade de posições possíveis é dada por (`CURVEMODE_MAX` - `CURVEMODE_MIN`).

`CURVE_MIN`- Define quão pra esquerda a curva pode ir
`CURVE_MAX` - Define quão pra direita a curva pode ir
`CURVE_INCREMENT` - O quanto é adicionado ou reduzido do valor de curva ao clicar nos botões da interface
`CURVE_CHANGE_RATE` - Quanto tempo ele demora para chegar no valor final

### Bike
Define as configurações relacionadas à bicicleta
`WHEEL_RADIUS` - Define o raio da roda da bicicleta

### Graphs (VERIFICAR)
Define as configurações relacionadas a como os gráficos serão exibidos na interface 
`GRAPH_POWER_MIN`
`GRAPH_POWER_MAX`

### Visual
Quanto ele multiplica a velocidade para aumentar o *feeling* de alta velocidade na Unity
`VISUAL_SPEED_MULTIPLIER` - Quantidade que é multiplicada

## Atributes
Representam os valores relacionados ao trajeto.
- **Speed**
	- `speedCurrent` - Velocidade atual naquele período do trajeto. Esse valor é alterado com base no `SPEED_CHANGE_RATE` por segundo até atingir o `speedTarget`
	- `speedTarget` - Velocidade final desejada que o `speedCurrent` deve alcançar
- **Angle**
	- `angleCurrent` - Ângulo atual naquele período do trajeto. Esse valor é alterado com base no `ANGLE_CHANGE_RATE` por segundo até atingir o `angleTarget`.
	- `angleTarget` - Ângulo final desejado que o `angleCurrent` deve alcançar
- **Power**
	- `powerCurrent` - Potência atual naquele período do trajeto. Esse valor é alterado com base no `POWER_CHANGE_RATE` por segundo até atingir o `powerTarget`
	- `powerTarget` - Potência final desejada que o `powerCurrent` deve alcançar
- **Curve**
	- `curveCurrent` - Ângulo da curva atual naquele período do trajeto. Esse valor é alterado com base no `CURVE_CHANGE_RATE` por segundo até atingir o `curveTarget`.
	- `curveTarget` - Ângulo da curva final desejado que o `curveCurrent` deve alcançar
	- `curveMode` - Ponto da interpolação usado para calcular o `curveCurrent`
### Coroutines
`powerOverTimeCoroutine` - Serve para armazenar a corrotina que ajusta o valor de power porque o valor do passo que ela utiliza é configurável pelo usuário em Runtime

### Getters
`SpeedCurrentMPS` - Retorna o `speedCurrent` convertida de RPM para m/s
`SpeedCurrentRPM` - Retorna o `speedCurrent`
`SpeedTargetMPS` - Retorna o `speedTarget` convertido de RPM para m/s
`SpeedTargetRPM` - Retorna o `speedTarget`
`SpeedCurrentNormalized` - Retorna a velocidade atual normalizada entre 0 e 1 (`speedCurrent` / `SPEED_MAX`)
`SpeedTargetNormalized` - Retorna a velocidade alvo normalizada entre 0 e 1 (`speedTarget` / `SPEED_MAX`)
`VisualSpeedCurrentMPS`
`VisualSpeedTargetMPS`