# Documentation-Engine
Registrar a Engine do Prof. Victor A. P. de Oliveira, na disciplina de POO em C++, no IFPB, é essencial para divulgar o conhecimento na Engenharia de Computação.

![image](uml_EngineASCII.svg)
<hr>

# Tutorial de como usar a Engine
Na sua primeira implementação básica é possivel que gere um erro, com isso, podendo não monstrar sua funcionalidade ou que execute apenas dando um aviso. <br/> <br/>
![image](https://github.com/LucasSTDev/Documentation-Engine/assets/116840737/82b4f27e-a8f4-4403-b8a1-8469526c5d34) <br/>

~~~c++
g++ -o game .cpp ASCII_Egine/.cpp && ./game
~~~
1. Explicação do comando: O "g++" Invoca o compilador gcc, "-o game" define o nome do executavel como "game"(O nome "game" pode ser o de sua preferência), *.cpp ASCII_Engine/.cpp são os arquivos que serão compilados. O código-fonte do programa está em um arquivo chamado .cpp e também em arquivos na pasta ASCII_Engine/. <br>

2. Execução:
&& ./game: Se a compilação for bem-sucedida (sem erros), o programa será executado. O && é um operador que indica que o próximo comando será executado se o anterior for executado sem erros. ./game é o comando que executa o programa compilado. <br/> <br/>
![image](https://github.com/LucasSTDev/Documentation-Engine/assets/116840737/9af01a8c-1eb4-4b4e-a1a1-a02a7b043b86)

Você pode lidar com esses avisos/erros de duas maneiras, uma delas é deletando os arquivos da classe sound(.cpp e o .hpp) 
1. Primeiro você entre no diretorio onde está a Engine e execute esse comando:

~~~c++ 
rm Sound.cpp Sound.hpp
~~~

Após fazer isso você pode checar se os arquivos foram excluídos com o comando:
~~~c++
tree
~~~
![image](https://github.com/LucasSTDev/Documentation-Engine/assets/116840737/9541b40a-3262-4a91-bea6-094eb9e54c34)

Tendo feito isso, execute o arquivo do seu jogo novamente:
~~~c++
./game
~~~
![image](https://github.com/LucasSTDev/Documentation-Engine/assets/116840737/6c504d85-eccc-47d2-a831-3839389b40b4)

<br/>
Faça o dowload do utilitario mpg123.

~~~sh
sudo apt-get install mpg123
~~~

ou,

~~~sh
sudo yum install mpg123
~~~
<br/>

Para ter uma implementação de som na engine vocé deve dividir o comdigo aseguir em arquivos .cpp .hpp , na mesma pasta da engine
<br/>
![image](https://github.com/D4Fi/Engine-games-C-/assets/139288494/ea54c45b-2eb2-43ee-89c5-937b9ffbce9d)<br/>
![image](https://github.com/D4Fi/Engine-games-C-/assets/139288494/226aff54-4d6e-4295-8b8b-a5c7b2efd0db)<br/>
![image](https://github.com/LucasSTDev/Documentation-Engine/assets/116840737/325868ae-8558-4006-93d1-351a749cb0d8)



* Classe Abstrata: "RenderBase" -> Mãe de Fase; ObjetoDeJogo; SpriteBase, Sprite, SpriteAnimado, SpriteBuffer e TextSprite.
+ Métodos puro: init -> Sem implementação. 
+ Métodos puro: update -> Sem implementação.
+ Métodos puro: draw -> Responsável por desenhar o sprite em determinada posição da matriz. (Sprite,nLinha,nColuna)

* Classe Abstrata: "Fase" -> Responsável por guardar o spite referente ao cenáiro do nível do jogo. (Nome, Sprite/SpriteAnimado) 
+ Método: draw -> Desenha um sprite na matriz. (tela, nLinha, nColuna) 
+ Método: getName -> Retorna o nome do sprite do background.
+ Método puro: run -> Sem implementação.
+ Método: show -> Mostra um print da tela. (SpriteBuffer tela)
+ Método: update -> Percorre a matriz background(tela). 

* Classe: "ObjetoDeJogo" - > Manipulações dos obejtos dentro do jogo, nela irá movimentar, decidir se um objeto deve
* ser parado de desenhando na tela e verificar a colisão dos objetos.
+ Método: construtor -> Os construtores são semelhantes, porém recebem vários tipos de Sprite diferente. (Nome, tipoSprite, nLinha, nColuna) 
+ Método: operator= -> Aloca um ponteiro para o tipo de sprite passado. (ObjetoDeJogo objeto) 
+ Método: colidecom -> Cuida da colisão do objeto, verifica se existe sobreposição de objetos nas posições verticais e horizontais na matriz. 
+ Retorna true se a posição estiver ocupada e false se não estiver. (ObjetoDeJogo) 
# Métodos de movimentação: 
+ Método: moveTo: Move o sprite para uma posição linha e coluna especificada na matriz. (pLinha,pColuna)
+ Método: moveLeft -> Move o sprite para uma coluna à esquerda na matriz.  
+ Método: moveRight -> Move o sprite para uma coluna à direita na matriz.
+ Método: moveUP -> Move o sprite para uma linha acima na matriz.
+ Método: moveUP -> Move o sprite para uma linha abaixo na matriz.
# Esses métodos não apagam o objeto, eles apenas atribuem verdadeiro/falso ao atributo active do objeto. 
# Se for verdadeiro, o objeto continua sendo desenhando, caso seja falso, o objeto não é mais desenhado.
+ Método: ativarObj -> Atribui true ao atributo active.
+ Método: desativarObj -> Atribui false ao atributo active.
+ Método: getName -> Retorna o nome do ObjetoDeJogo. 
+ Método: getPosL -> Retorna a posição da linha do ObjetoDeJogo.
+ Método: getPosC -> Retorna a posição da coluna do ObjetoDeJogo.
+ Método: getSpriprite -> Retorna o sprite de ObjetoDeJogo.

* Classe Abstrata: "SpriteBase" -> Mãe de Sprite, SpriteAnimado, SpriteBuffer e TextSprite. (nLinhainha, nColuna)
+ Métodos puro: putAt -> Sem implementações.
+ Método puro: getLinha -> Sem implementações 
+ Método puro: whoaim -> Sem implementações.
+ Método: getLargura -> Retorna o valor inclusivo da quantidade de colunas.
+ Método: getAltura -> Retorna o valor inclusivo da quantidade de linhas.

* Classe: "Sprite" -> Classes para sprite estáticos.
+ Método: puAt -> Posiciona um sprite em uma linha e coluna. (Sprite, nLinha, nColuna) 
+ Método: loadFromFile -> Abre um arquivo com o nome passado como argumento e carrega o sprite apartir dele. (String/referência/referência,) 
+ Método: whoaim -> Retorna uma string referente ao nome da classe.

* Classe: "SpriteAnimado" -> Classe para sprites que tem mais frames.
+ Método: operator[] -> Retorna um sprite em uma determinada posição. (index) 
+ Método: operator<< -> Faz um print no fluxo de saída e retona a saida dos sprites. (ostream out&, SpriteBuffer) 
+ Método: whoaim -> Retorna uma string referente ao nome da classe.
+ Método: getLinha -> Retorna um um SpriteAnimado em uma linha informada 
+ Método: size -> Retorna inteiro de quantidade de sprites em um vetor.

* Classe: "SpriteBuffer" -> Cria uma matriz de tamanho. (nLinha, nColuna)
+ Método: clear -> a função redefine o buffer do sprite (sprt) para um estado vazio, onde todas as linhas são preenchidas com espaços em branco.
+ Método: putAt -> Posiciona um sprite em uma posição da matriz. (Sprite, nLinha, nColuna)
+ Método: whoaim -> Retorna o nome da Classe.
+ Método: getLinha -> Retorna um sprite em uma linha. (nLinha)


* Classe: "TextSprite" -> Classe para sprites de conjunto de texto.
+ Método: whoaim -> Retorna o nome da Classe. 
+ Método: operator<< -> Mostra um print do texto e retona o texto. (Ponetiro de saida, Texto)
+ Método: getLinha -> Verifica se o texto está na linha 0, se estiver retona o texto.
+ Método: putAt -> Coloca um TextSprite em uma posição linha e coluna. (TextSprite, nLinha, nColuna) 





