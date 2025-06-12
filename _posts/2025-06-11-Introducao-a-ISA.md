---
title: Introdução ao nível de arquitetura de conjunto de instruções (ISA)
date: 2025-06-11 14:11:10 -0300
categories: [Arquitetura de Computadores, ISA]
tags: [arquitetura, introdução, isa, instruções, níveis]
author: koiyae
---

### Introdução

Este é o primeiro de uma série de artigos em que pretendo falar sobre arquitetura de computadores para fins de aprendizado e transmissão de conhecimento. Aqui, por conveniência e gosto pessoal, apresento uma breve introdução ao nível de arquitetura de conjunto de instruções (ISA), que será aprofundado em artigos posteriores.

### O que é um computador?

Antes de partirmos para o que é uma ISA, é necessário resumir, ainda que de forma bem superficial, o que é um computador.

Um computador é tão-somente uma máquina feita para resolver ou ajudar em tarefas humanas. Trata-se de uma máquina primitiva, a sua única tarefa real é realizar cálculos rapidamente, além de ser capaz de entender apenas 0s (transistor desligado) e 1s (transistor ligado).

Dado tal fato, você pode estar se perguntando: como, então, conseguimos realizar tarefas complexas, a exemplo de transmissão de vídeo e execução de jogos online? A resposta está na palavra **abstração**. Que é essa dita abstração? É simplesmente a organização de um computador em várias camadas, sendo cada camada superior responsável por abstrair operações mais complexas do nível abaixo e transformá-las em algo mais legível e amigável para o ser humano.

Antes de prosseguirmos, vale compreender como funciona a abstração em computadores na prática. Imagine uma escada: cada degrau representa um nível de complexidade. No topo, temos linguagens e interfaces próximas da forma como pensamos e escrevemos. Mais abaixo, instruções menos intuitivas, até chegar, por fim, aos sinais elétricos que o computador real entende – tensões de 0V ou 5V, representadas pelos valores 0 e 1, respectivamente. Observe o esquema abaixo:

<div style="font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; margin: 20px 0; padding: 20px; border-radius: 15px;">
    <div style="background: rgb(210, 210, 210); border-radius: 20px; padding: 30px; box-shadow: 0 20px 40px rgba(0,0,0,0.1); max-width: 600px; margin: 0 auto;">
        <div style="text-align: center; font-size: 28px; font-weight: bold; color: #2d3748; margin-bottom: 30px; background:rgb(44, 44, 44); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;">
            🖥️ Níveis de Computação
        </div>
        
        <div style="margin-bottom: 20px; border-radius: 15px; padding: 20px; color: white; background: linear-gradient(135deg, #8b5cf6, #7c3aed); box-shadow: 0 4px 15px rgba(0,0,0,0.1);">
            <div style="font-size: 18px; font-weight: bold; margin-bottom: 10px;">Máquina virtual nível n - Super Alto Nível</div>
            <div style="font-family: 'Courier New', monospace; font-size: 14px; background: rgba(0,0,0,0.2); padding: 8px 12px; border-radius: 8px; margin: 8px 0; border-left: 4px solid rgba(255,255,255,0.5);"># Código em AppleScript<br>if age ≥ 18 then display dialog "Adulto"<br></div>
            <div style="font-size: 13px; opacity: 0.9; margin-top: 8px;">🚀 Frameworks, bibliotecas, ferramentas drag-and-drop, IA etc.</div>
        </div>
        
        <div style="text-align: center; font-size: 24px; color: #4a5568; margin: 10px 0;">
            ⬇️
            <div style="font-size: 20px; font-weight: bold; color:rgb(0, 0, 0); margin-top: 5px;">Interpretador/Framework</div>
        </div>
        
        <div style="margin-bottom: 20px; border-radius: 15px; padding: 20px; color: white; background: linear-gradient(135deg, #10b981, #06d6a0); box-shadow: 0 4px 15px rgba(0,0,0,0.1);">
            <div style="font-size: 18px; font-weight: bold; margin-bottom: 10px;">Máquina virtual nível 3 - Linguagens de Alto Nível</div>
            <div style="font-family: 'Courier New', monospace; font-size: 14px; background: rgba(0,0,0,0.2); padding: 8px 12px; border-radius: 8px; margin: 8px 0; border-left: 4px solid rgba(255,255,255,0.5);">int idade = 25;<br>if (idade >= 18) printf("Adulto");</div>
            <div style="font-size: 13px; opacity: 0.9; margin-top: 8px;">💻 C, Java, Python etc.</div>
        </div>
        
        <div style="text-align: center; font-size: 24px; color: #4a5568; margin: 10px 0;">
            ⬇️
            <div style="font-size: 20px; font-weight: bold; color:rgb(0, 0, 0); margin-top: 5px;">Compilador/Interpretador</div>
        </div>
        
        <div style="margin-bottom: 20px; border-radius: 15px; padding: 20px; color: white; background: linear-gradient(135deg, #3b82f6, #1d4ed8); box-shadow: 0 4px 15px rgba(0,0,0,0.1);">
            <div style="font-size: 18px; font-weight: bold; margin-bottom: 10px;">Máquina virtual nível 2 - Assembly</div>
            <div style="font-family: 'Courier New', monospace; font-size: 14px; background: rgba(0,0,0,0.2); padding: 8px 12px; border-radius: 8px; margin: 8px 0; border-left: 4px solid rgba(255,255,255,0.5);">MOV AX, 25<br>CMP AX, 18<br>JGE adulto</div>
            <div style="font-size: 13px; opacity: 0.9; margin-top: 8px;">🔧 Comandos simbólicos</div>
        </div>
        
        <div style="text-align: center; font-size: 24px; color: #4a5568; margin: 10px 0;">
            ⬇️
            <div style="font-size: 20px; font-weight: bold; color:rgb(0, 0, 0); margin-top: 5px;">Assembler</div>
        </div>
        
        <div style="margin-bottom: 20px; border-radius: 15px; padding: 20px; color: white; background: linear-gradient(135deg, #f59e0b, #d97706); box-shadow: 0 4px 15px rgba(0,0,0,0.1);">
            <div style="font-size: 18px; font-weight: bold; margin-bottom: 10px;">Máquina virtual nível 1 - Linguagem de Máquina</div>
            <div style="font-family: 'Courier New', monospace; font-size: 14px; background: rgba(0,0,0,0.2); padding: 8px 12px; border-radius: 8px; margin: 8px 0; border-left: 4px solid rgba(255,255,255,0.5);">10110000 00011001<br>00111001 00010010<br>01110101 00000100</div>
            <div style="font-size: 13px; opacity: 0.9; margin-top: 8px;">🔢 Apenas 0s e 1s</div>
        </div>
        
        <div style="text-align: center; font-size: 24px; color: #4a5568; margin: 10px 0;">
            ⬇️
            <div style="font-size: 20px; font-weight: bold; color:rgb(0, 0, 0); margin-top: 5px;">Circuitos Eletrônicos</div>
        </div>
        
        <div style="margin-bottom: 20px; border-radius: 15px; padding: 20px; color: white; background: linear-gradient(135deg, #ef4444, #dc2626); box-shadow: 0 4px 15px rgba(0,0,0,0.1);">
            <div style="font-size: 18px; font-weight: bold; margin-bottom: 10px;">Máquina nível 0 (Computador real) - Hardware</div>
            <div style="font-family: 'Courier New', monospace; font-size: 14px; background: rgba(0,0,0,0.2); padding: 8px 12px; border-radius: 8px; margin: 8px 0; border-left: 4px solid rgba(255,255,255,0.5);">⚡ 5V = 1, 0V = 0</div>
            <div style="font-size: 13px; opacity: 0.9; margin-top: 8px;">🔌 Sinais elétricos, transistores, circuitos integrados</div>
        </div>
    </div>
</div>

Um computador com múltiplos níveis funciona como diferentes máquinas virtuais, cada uma com a sua linguagem específica. Apenas a linguagem do nível mais baixo é executada diretamente pelo hardware (utilizarei esse termo para me referir aos circuitos eletrônicos de agora em diante), enquanto as demais precisam ser interpretadas ou traduzidas (compiladas) para níveis inferiores. Isso é bom para o programador que trabalha em níveis superiores, porque ele não precisa se preocupar com esses processos de tradução, já que a arquitetura do sistema garante que seus programas serão executados, independentemente de como isso acontece internamente.

### Nível de arquitetura de conjunto de instruções

Agora que sabemos o que é um computador, é importante ressaltar que o esquema apresentado anteriormente trata-se apenas da ponta do iceberg em relação a onde pretendemos chegar. Computadores modernos são, na verdade, constituídos por alguns outros níveis não apresentados, como é o caso do nível de microarquitetura – que será tratado em outra ocasião – e o nível ISA (Instruction Set Architecture), do qual trataremos agora.

Criado com o intuito de padronizar a fabricação de processadores e torná-los compatíveis entre si, a ISA é uma especificação meramente abstrata que define a interface de comunicação entre hardware e software, sendo um modelo de programação oferecido pelo processador e o designador do comportamento do hardware. É a linguagem comum compreendida por compiladores e hardware. Alinhando-nos a Tanenbaum, podemos dizer que o código de ISA é o que um compilador produz.

Tendo isso em mente, é possível dizer que a ISA é responsável por definir os tipos de instruções disponíveis, os tipos de operações, modos de endereçamento, modos de operação (como usuário e kernel, que serão abordados em outros artigos), além de como o hardware se comporta do ponto de vista do programador. Alguns exemplos de ISA são x86-64, ARM e RISC-V. Pela conveniência de ser o meu ponto central de estudos, focarei principalmente na ISA RISC-V.

#### Confusão entre ISA e Assembly

Na grande maioria dos casos concretos, o código produzido pelos compiladores está em linguagem Assembly, mas disso pode surgir a confusão de que o Assembly é a própria ISA. Podemos dizer que a ISA é a especificação, isto é, define o comportamento, enquanto o Assembly é a implementação, ou seja, a concretude da especificação, de certo modo. Recorrerei à simples analogia de que a ISA está para o Assembly do mesmo modo que a gramática está para a sintaxe, pois enquanto aquela define o idioma, suas regras e comportamentos, esta define as palavras escritas. Podem existir diversos tipos de sintaxe Assembly dentro de uma única ISA, como no caso do x86-64 (Intel) e do x86-64 (AT&T), que são sintaxes diferentes porém intercomunicáveis.

### Implementações

Como dito anteriormente, focarei na ISA RISC-V. Observe a implementação abaixo:

<div style="font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; margin: 20px 0; padding: 20px; border-radius: 15px;">
    <div style="background: rgb(210, 210, 210); border-radius: 20px; padding: 30px; box-shadow: 0 20px 40px rgba(0,0,0,0.1); max-width: 600px; margin: 0 auto;">
        <div style="text-align: center; font-size: 28px; font-weight: bold; color: #2d3748; margin-bottom: 30px; background:rgb(44, 44, 44); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text;">
            🖥️ Assembly RISC-V
        </div>
        
        <div style="margin-bottom: 20px; border-radius: 15px; padding: 20px; color: white; background: linear-gradient(135deg, #3b82f6, #1d4ed8); box-shadow: 0 4px 15px rgba(0,0,0,0.1);">
            <div style="font-size: 18px; font-weight: bold; margin-bottom: 10px;">Máquina virtual nível 2 - Assembly RISC-V</div>
            <div style="font-family: 'Courier New', monospace; font-size: 14px; background: rgba(0,0,0,0.2); padding: 8px 12px; border-radius: 8px; margin: 8px 0; border-left: 4px solid rgba(255,255,255,0.5);">li x5, 15        # Carrega 15 no registrador x5<br>li x6, 27        # Carrega 27 no registrador x6<br>add x7, x5, x6   # x7 = x5 + x6 (soma)<br>mv a0, x7        # Move resultado para o argumento</div>
            <div style="font-size: 13px; opacity: 0.9; margin-top: 8px;">🔧 Mnemônicos legíveis, instruções Assembly RISC-V</div>
        </div>
    </div>
</div>

O código Assembly realiza a soma de dois números (15 + 27) através de quatro instruções básicas:
Primeiro, as instruções `li x5, 15` e `li x6, 27` carregam os valores constantes nos registradores `x5` e `x6`, respectivamente. Em seguida, `add x7, x5, x6` executa a soma propriamente dita, armazenando o resultado (42) no registrador `x7`. Por fim, `mv a0, x7` move o resultado para o registrador `a0`, seguindo a convenção de chamada RISC-V, em que `a0` é usado para retorno de valores. Isso demonstra que a ISA RISC-V possui alguns princípios fundamentais, como instruções simples e uniformes, operações load/store explícitas e uso eficiente do banco de 32 registradores, como toda boa ISA. A ISA RISC-V define exatamente como cada instrução deve ser codificada em binário e executada pelo hardware, criando uma interface clara entre ele e o software.
