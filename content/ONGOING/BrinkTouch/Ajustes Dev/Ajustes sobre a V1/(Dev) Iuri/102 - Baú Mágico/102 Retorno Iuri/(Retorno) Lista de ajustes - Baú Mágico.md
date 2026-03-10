### Legenda
Pequeno: 🟢
Grande: 🟡
Extra (pago): 🔴

Prazos possíveis: 0,5 dia//1 dia//1,5 dia//2 dias//3+ dias
- Se uma coisa é questão de minutos, organize pra me responder que X coisas juntas custam 0,5 dia, porque a entrega vai ser toda de uma vez mesmo, mas eu preciso saber o que esperar no fim de prazos maiores;
- Devolva os ==comentários== com ==realce==;

### Ajustes
- [x] (PRAZO) [^2]Todos os textos ou palavras devem estar em caixa alta, pois é um aplicativo voltado para Educação Infantil. 
      -  Já feito, pendente as mudanças do header do gerenciador
- [x] (PRAZO) [^3]No Menu, quando não houver tradução de libras para o aplicativo, a habilitação do recurso não deve estar disponível (aparecer em cor mais clara e sem opção de mudança do status do botão - on/off).
      - Gerenciador
- [x] (PRAZO) Para fechar/retrair o menu, a setinha deveria apontar para cima.
      - Única seta no menu é no gerenciador, que é externa ao jogo e deve ser integrada na animação de subir e descer a barra
- [x] (PRAZO) Se você não sai do jogo e só muda de dificuldade ou de quantidade de jogadores, a ordem dos brinquedos sempre é a mesma. Programar que seja aleatório a sequência dos brinquedos em cada partida.
      - Teste em 53 sorteios, nenhum resultado idêntico, saindo do jogo ou não
- [ ] (0.1)🟢 Deve ter um botão no menu que permita mudanças de dificuldade ou jogadores. Da forma que está, tem que terminar a partida ou sair do programa para mudar.
      - ==Está como foi combinado na primeira entrega, quando tiver a referencia da UI/UX e o sprite do botão de voltar (esse jogo não possui isso) pode ser feito rapidamente==
- [ ] (0.05)🟢 [^4]A narração das “formas de madeira” está errada. Está como “fôrma”, com o som fechado, como “forma de bolo”. Substituir por “jogo de madeira”.
      ==- Troca rápida quando tiver o áudio na mão==
- [ ] (0.2)🟢 No nível médio, é uma vida a menos. Ao invés de aparecer um coração apagado, poderia somente ter 4 corações. Da mesma forma que para o nível difícil - só aparecer 3 corações.
    - ==Os corações vazios são travados na imagem da UI BD_time ![[Pasted image 20260309183416.png|231]]== 
    - ==Seria necessário alterar a imagem base e refazer o funcionamento da perda de vida atual, nada muito complexo, só *time consuming*==
- [ ] (0.1)🟢 Aumentar a velocidade do nível médio e do nível difícil.
      ==- Facilmente alterável, definir o quanto quer aumentar (porcentagem, quantidade) valores atuais: ![[Pasted image 20260309183726.png|394]]==
- [ ] (0.2)🟢 A imagem do cavalo de pau está muito pequena em relação aos demais brinquedos. Destacar também o bambolê. Rever a proporção das imagens dos brinquedos.
      ==- Todas as imagens são do mesmo tamanho e utilizam o mesmo canvas, essa alteração é mais relacionada a criação do sprite do que a alteração in-game, se for pra mudar o tamanho dinamicamente com o tipo de imagem, vai ser custo extra porque tem que refazer toda a parte de sorteio pra interpretar tamanho e sprite, tendo o sprite é fácil de trocar, mas demanda múltiplos testes pra validar o posicionamento novo, tamanho das imagens atuais são 512x512 e o tamanho na UI dos baús são 268x268px==
- [ ] (0.1)🟢 Rever a pontuação: mesmo não errando nada, não se consegue atingir a pontuação da medalha de bronze em determinadas partidas.
      ==- Possivelmente atrelado ao fato de que não se perde nada a não ser tempo de jogo quando não interage (não perde vida nem ganha ponto quanto não interage, como definido na definição do projeto) e tem que estar entre 50 e 70% de acertos pra pontuação triggar a de bronze, valores atuais: ![[Pasted image 20260309184134.png]]==
      - ![[Pasted image 20260309184338.png]]
- [x] (PRAZO) Ainda finaliza as vezes com a pontuação sobreposta nas cartas.
	- == ? falta detalhes, acredito ser de outro jogo==
- [ ] (0.5)🟡 [^1]Apresentar sempre mensagens positivas para a criança, mesmo que ela não consiga nem uma medalha. Ao invés de “Poxa, não foi dessa vez!”, alterar para “Continue jogando e melhore sua pontuação”.
	- ==É uma mudança significativa nesse caso por ter que refazer todo o sorteio final e refazer a localização do jogo==



[^1]: Já foi pedido/corrigido no ajuste que pede a tabela final com respostas fixas.
[^2]: A questão é que isso envolve os textos do gerenciador também, a barra de tutorial por exemplo. Então se você passar todo o seu app e ele estiver com todos os textos em caixa alta mesmo, tá correto, só avisa.
[^3]: Gerenciador, novamente.
[^4]: Me dá o prazo considerando que você tem o áudio.
