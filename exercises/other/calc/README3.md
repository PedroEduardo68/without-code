# P4 Calc

Esse software possibilita a realização de cálculos através do plano de dados de uma pacote. Basicamente, nesse software terá dois cabeçalhos, o cabeçalho normal de rede o Ethernet e depois delete tera o cabeçalho que denomina calculo. Esse cabeçalho tem o tipo de 0x1234 na ethernet.

Um pacote é gerado com esse cabeçalho e é encaminhado para um switch, que realiza as operações e devolve o pacote com um valor no "Result".


            0                1                  2              3
    +----------------+----------------+----------------+---------------+
    |      P         |       4        |     Version    |     Op        |
    +----------------+----------------+----------------+---------------+
    |                              Operand A                           |
    +----------------+----------------+----------------+---------------+
    |                              Operand B                           |
    +----------------+----------------+----------------+---------------+
    |                              Result                              |
    +----------------+----------------+----------------+---------------+



* P é em  ASCII 'P' (0x50)
* 4 é em  ASCII '4' (0x34)
* Versão atual 0.1 (0x01)
* Op é as operações que pode ser executada:
* '+' (0x2b) Result = OperandA + OperandB
* '-' (0x2d) Result = OperandA - OperandB
* '&' (0x26) Result = OperandA & OperandB
* '|' (0x7c) Result = OperandA | OperandB
* '^' (0x5e) Result = OperandA ^ OperandB


Para executar programa P4, é necessário iniciar o ambiente com o comando:

    make

Depois o host 1 irá executar o arquivo em python calc.py esse arquivo gera o cabeçalho acima encaminha o pacote para o switch e recebe o valor.

    h1 python calc.py

Para realizar o cálculo basta digitar os dois operandos e a operação necessária, conforme o comando abaixo:

    > 1+1
    2


Para finalizar a análise, basta executar o comando "quit" no mininet e ao voltar ao terminal executar os dois comandos abaixo:

    make stop
    make clean