<p align="center"> <img src="https://media.giphy.com/media/l41YvpiA9uMWw5AMU/giphy.gif"/> 


# Portfólio Prático de Infraestrutura de Redes LAN Corporativas — InovaTech Soluções

---

## Identificação Acadêmica
* **Instituição de Ensino:** Centro Universitário do Planalto Central Apparecido dos Santos (UNICEPLAC)
* **Curso:** Engenharia de Software
* **Disciplina:** Comunicação de Dados e Redes de Computadores
* **Orientador:** Profº Hudson Neves

##  Equipe do Projeto
* Anna Gabriela Dimas Furtado
* Brenda Sousa Costa 
* Nikoly Karoline De Paula Pereira
* Maria Vitória Pereira dos Santos 
* Matheus Souza de Jesus
* Thallys Maycon de Jesus Silva
  
---

## Vídeo de Apresentação

[Assista aqui](https://youtu.be/o-55s1lKCqI)

---

## Descrição

Projeto prático de infraestrutura de rede **LAN corporativa** simulado no **Cisco Packet Tracer**, desenvolvido para a empresa fictícia **InovaTech Soluções**. A empresa modernizou sua infraestrutura de rede local para atender à expansão de suas operações, com foco em alta disponibilidade (LACP/STP), segmentação por VLANs e roteamento Layer 3.

Esta atividade integrada consolida o aprendizado prático de estruturação, configuração e validação de redes locais corporativas, aplicando segmentação rigorosa por VLANs, roteamento entre redes, automação de serviços essenciais e alta disponibilidade com agregação de links. O documento segue os padrões exigidos para o registro de arquiteturas corporativas, servindo de base para auditorias, manutenção e futuras expansões.

## Objetivos

**Objetivo geral:** projetar uma rede corporativa de grande porte, altamente funcional, resiliente e segura, aplicando segmentação por VLANs, roteamento Inter-VLAN, automação de serviços essenciais (DHCP/DNS) e alta disponibilidade via agregação de links.

**Problema que o sistema resolve:** organiza e isola o tráfego entre os departamentos da InovaTech Soluções (Diretoria, TI, Financeiro e Atendimento), garante redundância dos links críticos e aplica controle de acesso entre setores sensíveis, evitando falhas e vazamento de dados entre segmentos da rede.

**Público-alvo:** A ser definido pela equipe

---

## Funcionalidades Implementadas

- **Switches Layer 3 (Core)** — Roteamento Inter-VLAN ativado no núcleo da rede.
- **Agregação de Links (EtherChannel/LACP)** — Links trunk agrupados em alta disponibilidade entre switches de acesso e núcleo.
- **Automação DHCP/DNS e Relay** — Distribuição dinâmica de IPs com apoio de `ip helper-address`.
- **Segurança Perimetral (ACL)** — Bloqueio de tráfego originado no Atendimento (VLAN 40) direcionado ao Financeiro (VLAN 30).

### Itens da infraestrutura

- **Switches Layer 3 (Core):** 2 unidades — `MultilayerSwitch0` e `MultilayerSwitch1` (roteamento central, alta disponibilidade e gateway das VLANs)
- **Switches Layer 2 (Acesso):** 4 unidades — `Switch0` a `Switch3` (conexão das estações de trabalho por setor)
- **Servidores locais (Data Center):** 3 unidades
  - `Server0` — Servidor DHCP/DNS
  - `Server1` — Servidor de Arquivos
  - `Server2` — Servidor de Banco de Dados
- **Dispositivos finais:** 30 a 40 unidades (PCs e laptops), totalizando de 40 a 50 dispositivos na rede

---

## Tecnologias Utilizadas

- Cisco Packet Tracer 
- Cisco IOS (switches Layer 2 e Layer 3)
- Protocolos: LACP (EtherChannel), roteamento Inter-VLAN, DHCP/DNS, ACL estendida

---

## Arquitetura da Solução

A organização da rede segue uma hierarquia estruturada em camadas para otimizar o fluxo de tráfego, mitigar domínios de broadcast e garantir redundância:

- **Camada de Núcleo (Core):** concentra o entroncamento (trunking) dos switches de acesso e executa o roteamento interno entre as redes virtuais (Inter-VLAN Routing).
- **Camada de Acesso:** conecta os dispositivos finais às respectivas VLANs departamentais por meio de portas de acesso dedicadas.
- **Mapa de topologia:** a disposição física e lógica está representada no arquivo de simulação `Topologia_InovaTech_Grupo5.pkt`, evidenciando as interconexões por cabos Gigabit Ethernet e Fast Ethernet.

![Topologia da rede](<img width="1069" height="710" alt="Captura de tela 2026-09-10 160749" src="https://github.com/user-attachments/assets/0aa09bce-312c-4ecb-8e2b-8bd1cea59646" />
)

### Detalhes técnicos de configuração

- **Roteamento Inter-VLAN:** ativado no núcleo através do comando `ip routing` e interfaces virtuais (`interface vlan X`) configuradas com os respectivos endereços de gateway.
- **Agregação de Links (EtherChannel/LACP):** implementação de EtherChannel (LACP no modo *active*) nos links entre os switches de acesso e o núcleo (`channel-group 1` e `10`), garantindo maior largura de banda e tolerância a falhas.
- **Automação de endereçamento (DHCP e Relay):** o `Server0` distribui dinamicamente os endereços IP para todas as estações. O comando `ip helper-address` foi aplicado nas interfaces virtuais do switch Core para encaminhar as solicitações DHCP originadas nas VLANs remotas.
- **Políticas de segurança (ACL):** implementação de uma Lista de Controle de Acesso Estendida (ACL 100) no switch Core para isolar dados sensíveis:
  - Regra de bloqueio: o tráfego oriundo do Atendimento (`192.168.40.0/24`) com destino ao Financeiro (`192.168.30.0/24`) é negado (`deny ip`).
  - Regra de permissão: as demais comunicações corporativas válidas são permitidas (`permit ip any any`).

---

## Pré-requisitos

- Cisco Packet Tracer instalado (versão 9.x ou superior)

## Instalação

1. Faça o download deste repositório.
2. Baixe o arquivo `Topologia_InovaTech_Grupo5.pkt` contido no repositório.

## Como Executar

1. Abra o arquivo `Topologia_InovaTech_Grupo5.pkt` no Cisco Packet Tracer.
2. Aguarde a convergência dos protocolos (todas as luzes verdes nos cabos).
3. Abra qualquer estação final (PC ou Laptop) e mude a configuração de IP para DHCP. Confirme o recebimento do IP dinâmico da respectiva VLAN.
4. Para validar o roteamento, abra o *Command Prompt* em um PC da VLAN 10 e execute `ping 192.168.30.100`.
5. Para validar a ACL de segurança, abra o *Command Prompt* em um PC da VLAN 40 e execute `ping 192.168.30.100` (o tráfego deve ser bloqueado).

---

## Tabela de Endereçamento IP e VLANs

| Segmento / VLAN | Nome do Departamento | Faixa de IP (Sub-rede) | Gateway Padrão | Servidor DNS |
|---|---|---|---|---|
| VLAN 10 | Diretoria | 192.168.10.0/24 | 192.168.10.1 | 192.168.10.10 |
| VLAN 20 | TI / Infraestrutura | 192.168.20.0/24 | 192.168.20.1 | 192.168.10.10 |
| VLAN 30 | Financeiro | 192.168.30.0/24 | 192.168.30.1 | 192.168.10.10 |
| VLAN 40 | Atendimento | 192.168.40.0/24 | 192.168.40.1 | 192.168.10.10 |

A rede utiliza o esquema de endereçamento privado IPv4 baseado na sub-rede `192.168.X.0/24`, com máscara padrão `255.255.255.0`.

## Tabela de Portas e Alocação de VLANs

| Switch de Acesso | Interface / Porta | Função | VLAN Alocada |
|---|---|---|---|
| Switch0 | Fa0/1 – Fa0/8 | Conexão de PCs | VLAN 10 (Diretoria) |
| Switch1 | Fa0/1 – Fa0/7 | Conexão de Laptops | VLAN 20 (TI / Infra) |
| Switch2 | Fa0/1 – Fa0/8 | Conexão de PCs | VLAN 30 (Financeiro) |
| Switch3 | Fa0/1 – Fa0/7 | Conexão de Laptops | VLAN 40 (Atendimento) |

---

## Comandos de Auditoria

Comandos do Cisco IOS utilizados para auditar e verificar o estado operacional dos equipamentos de rede:

- `show vlan brief` — confirma o status ativo de todas as VLANs e o particionamento correto das portas de acesso.
- `show etherchannel summary` — valida a operação da agregação de links via LACP entre os switches de acesso e o núcleo, assegurando as flags SU (Layer 2/In-use).
- `show ip route` — apresenta a tabela de roteamento do switch Core, evidenciando as redes diretamente conectadas (C) para habilitar o roteamento Inter-VLAN.

![Saída do comando show vlan brief](<img width="769" height="706" alt="show vlan brief" src="https://github.com/user-attachments/assets/4bd493a1-3552-4b1b-831b-329d9b62826c" />)

![Saída do comando show etherchannel summary](<img width="830" height="714" alt="show etherchannel summary" src="https://github.com/user-attachments/assets/ad4defb3-f65b-4b01-9ea1-f951e27d3bdb" />
)

![Saída do comando show ip route](<img width="837" height="719" alt="show ip route" src="https://github.com/user-attachments/assets/ed6733f5-02e3-45e8-916f-11733b8b310e" />
)

---

## Exemplos de Uso / Evidências de Validação

**Validação do DHCP:** ao configurar uma estação final para obter IP via DHCP, ela recebe automaticamente o endereço da sub-rede correspondente à sua VLAN.

![Confirmação do recebimento dinâmico de IP via DHCP](<img width="943" height="708" alt="Confirmação DHCP" src="https://github.com/user-attachments/assets/9ddb6dbb-7d2b-453f-b0a6-ab19448f9414" />)

**Validação do roteamento Inter-VLAN (VLAN 10 → VLAN 30):**
```
C:\> ping 192.168.30.1

Reply from 192.168.30.1: bytes=32 time=1ms TTL=255
Reply from 192.168.30.1: bytes=32 time<1ms TTL=255
Reply from 192.168.30.1: bytes=32 time<1ms TTL=255
Reply from 192.168.30.1: bytes=32 time<1ms TTL=255

Ping statistics for 192.168.30.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

![Teste de comunicação permitida VLAN 10 para VLAN 30](<img width="566" height="326" alt="Captura de tela 2026-09-10 014356" src="https://github.com/user-attachments/assets/6d7ebbcb-733d-44a8-8b13-7d2d93b115c0" />) 

**Validação da ACL de segurança (VLAN 40 → VLAN 30, tráfego bloqueado):**
```
C:\>ping 192.168.30.100

Pinging 192.168.30.100 with 32 bytes of data:

Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 192.168.30.100:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss)
```

![Teste de isolamento por ACL VLAN 40 para VLAN 30](<img width="740" height="687" alt="Isolamento por ACL VLAN 40 para VLAN 30" src="https://github.com/user-attachments/assets/c33c84ab-75ff-4a2a-9528-5433a234a776" />)

---

## Estrutura do Projeto

```
InovaTech_Grupo5/
├── Topologia_InovaTech_Grupo5.pkt     # Arquivo oficial da topologia (Cisco Packet Tracer)
├── README.md                          # Documentação estruturada do projeto
└── Relatorio_Tecnico_InovaTech.pdf    # Relatório técnico formal com evidências e capturas de tela
```

## Relatório dos Entregáveis Obrigatórios

| Entregável | Conteúdo |
|---|---|
| 1. Repositório no GitHub | Repositório público com o arquivo oficial da topologia (`Topologia_InovaTech_Grupo5.pkt`), a documentação estruturada (`README.md`) e os blocos de comandos CLI salvos em texto para auditoria |
| 2. Relatório Técnico em PDF | Documento formal com introdução ao cenário, mapeamento técnico, evidências fotográficas e capturas de tela dos comandos de auditoria e dos testes de conectividade/DHCP |
| 3. Vídeo de Apresentação | Vídeo com a participação de todos os integrantes, contendo introdução da equipe, explicação da topologia e demonstração prática no Packet Tracer |

## Manutenção e Ferramentas de Gerenciamento

- **Revisão contínua:** a documentação deve ser atualizada sempre que houver alterações físicas ou lógicas na infraestrutura.
- **Ferramentas utilizadas:** Cisco Packet Tracer para modelagem e testes; GitHub para controle de versão; editores corporativos para exportação em PDF com layout institucional.

---

## Guia Passo a Passo para Execução dos Testes

1. Baixe o arquivo `.pkt` contido neste repositório e abra no Cisco Packet Tracer.
2. Aguarde a convergência dos protocolos (todas as luzes verdes nos cabos).
3. Abra qualquer estação final (PC ou Laptop) e mude a configuração de IP para DHCP. Confirme o recebimento do IP dinâmico da respectiva VLAN.
4. Para validar o roteamento, abra o *Command Prompt* em um PC da VLAN 10 e execute `ping 192.168.30.100`.
5. Para validar a ACL de segurança, abra o *Command Prompt* em um PC da VLAN 40 e execute `ping 192.168.30.100` (o tráfego deve ser bloqueado).

## Status do Projeto

Concluído (entregável acadêmico completo: repositório, relatório técnico e vídeo de apresentação)

## Melhorias Futuras

A ser definido pela equipe

## Licença

"Projeto acadêmico desenvolvido para fins educacionais na disciplina de Comunicação de Dados e Redes de Computadores
 — UNICEPLAC. Uso restrito aos fins do curso."

## Conclusão

O projeto demonstra a implementação de uma infraestrutura LAN corporativa segmentada por VLANs, com roteamento Inter-VLAN, agregação de links via LACP, distribuição dinâmica de endereços por DHCP e aplicação de ACLs para controle do tráfego entre departamentos. Os testes realizados no Cisco Packet Tracer comprovam o funcionamento dos principais serviços e mecanismos de segurança da rede.
