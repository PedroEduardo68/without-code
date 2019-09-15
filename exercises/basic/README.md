
# P4 BASIC

O Basic é um programa que deve encaminhar um pacote IPV4 até seu destino, tem o nome de basic, pois é a função mais básica programada no P4. Com ela é possível encaminhar um pacote de um host para outro.

Para analisar o funcionamento do programa, foi criado no mininet a seguinte topologia:
![pod-topo](./pod-topo/pod-topo.png)

Cabeçalhos que são reconhecidos no Parser do switches.

    header ethernet_t {
        macAddr_t dstAddr;
        macAddr_t srcAddr;
        bit<16>   etherType;
    }

    header ipv4_t {
        bit<4>    version;
        bit<4>    ihl;
        bit<8>    diffserv;
        bit<16>   totalLen;
        bit<16>   identification;
        bit<3>    flags;
        bit<13>   fragOffset;
        bit<8>    ttl;
        bit<8>    protocol;
        bit<16>   hdrChecksum;
        ip4Addr_t srcAddr;
        ip4Addr_t dstAddr;
    }

No processamento de entrada o pacote será avaliado pelo plano de dados através do IPv4 de destino presente no pacote. E desta forma retorna para qual porta e ações que deve se executada.

Pode ser a ação de encaminhara o pacote ou descartar.

Ação Encaminhamento - Encaminha o pacote para uma porta de saída, realiza a alteração dos MACs origem e destino, conforme vai trafegando pelo switch e decrementa o TLL do pacote.
Ação Drop - Descarta o pacote no momento que é executada.




Depois de editar o arquivo com o código P4, tem que ser analisado se está funcionando:

No terminal dentro pasta do "basic", executa o comando:

    make run

Para verificar se está funcionando normalmente esse programa, é realizado um teste de pinga entre os hosts. Segue o comando abaixo:

    mininet> h1 ping h2
    mininet> pingall

Para finalizar os testes, utilizam-se os comandos:

    make stop
    make clean

