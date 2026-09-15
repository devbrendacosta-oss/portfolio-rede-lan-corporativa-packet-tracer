# Portfólio Prático de Infraestrutura de Redes LAN Corporativas com Simulação em Cisco Packet Tracer

Projeto da disciplina de Engenharia e Infraestrutura de Redes — Cisco Packet Tracer.

Projeto prático de rede LAN corporativa com alta disponibilidade (LACP/STP), segmentação por VLANs e roteamento Layer 3, desenvolvido para a empresa fictícia **InovaTech Soluções**.

## Integrantes do Grupo

- Anna Gabriela Dimas Furtado
- Brenda Sousa Costa
- Nikoly Karoline De Paula Pereira
- Maria Vitória Pereira dos Santos
- Matheus Souza de Jesus
- Thallys Maycon de Jesus Silva

## Cenário da Empresa

A empresa InovaTech Soluções modernizou sua infraestrutura de rede local (LAN) para atender à expansão de suas operações. A topologia foi desenvolvida para suportar alta performance local, resiliência, automação de serviços e segurança no controle de tráfego entre departamentos.

## Vídeo de Apresentação

https://youtu.be/o-55s1lKCqI

## Topologia da Rede

Representação da topologia lógica implementada no Cisco Packet Tracer, contendo os switches de Core, Acesso, servidores do Data Center e estações finais.

<img width="1069" height="710" alt="Topologia da rede" src="https://github.com/user-attachments/assets/e8d334c3-8851-4950-a337-e92f0216d3cf" />

## Tabela de Portas e Alocação de VLANs

| Switch de Acesso | Interface / Porta | VLAN Alocada | Função / Departamento |
| --- | --- | --- | --- |
| Switch0 | Fa0/1 – Fa0/8 | VLAN 10 | PCs – Diretoria |
| Switch1 | Fa0/1 – Fa0/7 | VLAN 20 | Laptops – TI / Infraestrutura |
| Switch2 | Fa0/1 – Fa0/8 | VLAN 30 | PCs – Financeiro |
| Switch3 | Fa0/1 – Fa0/7 | VLAN 40 | Laptops – Atendimento |

## Tabela de Endereçamento IP e VLANs

| Segmento / VLAN | Faixa de IP (Sub-rede) | Gateway Padrão | Escopo / Departamentos |
| --- | --- | --- | --- |
| VLAN 10 (Diretoria) | 192.168.10.0/24 | 192.168.10.1 | Acesso restrito e servidores críticos |
| VLAN 20 (TI / Infra) | 192.168.20.0/24 | 192.168.20.1 | Admins de rede e suporte |
| VLAN 30 (Financeiro) | 192.168.30.0/24 | 192.168.30.1 | Estações financeiras e banco de dados |
| VLAN 40 (Atendimento) | 192.168.40.0/24 | 192.168.40.1 | Suporte operacional ao cliente |

## Comandos de Auditoria

Comandos do Cisco IOS utilizados para auditar e verificar o estado operacional dos equipamentos de rede:

- `show vlan brief` — confirma o status ativo de todas as VLANs e o particionamento correto das portas de acesso.
- `show etherchannel summary` — valida a operação da agregação de links via LACP entre os switches de acesso e o núcleo, assegurando as flags SU (Layer 2/In-use).
- `show ip route` — apresenta a tabela de roteamento do switch Core, evidenciando as redes diretamente conectadas (C) para habilitar o roteamento Inter-VLAN.

## Funcionalidades Implementadas

- **Switches Layer 3** — Roteamento Inter-VLAN ativado no núcleo da rede.
- **Agregação de Links (EtherChannel/LACP)** — Links trunk agrupados em alta disponibilidade.
- **Automação DHCP Relay** — Distribuição dinâmica de IPs com apoio de `ip helper-address`.
- **Segurança Perimetral (ACL)** — Bloqueio de tráfego originado no Atendimento (VLAN 40) direcionado ao Financeiro (VLAN 30).

## Evidências e Validação de Testes

### Automação DHCP

Confirmação do recebimento dinâmico de endereçamento IP nas estações de trabalho finais:

<img width="943" height="708" alt="Confirmação DHCP" src="https://github.com/user-attachments/assets/9ddb6dbb-7d2b-453f-b0a6-ab19448f9414" />

### Saídas dos Comandos de Auditoria

`show vlan brief`

<img width="769" height="706" alt="show vlan brief" src="https://github.com/user-attachments/assets/4bd493a1-3552-4b1b-831b-329d9b62826c" />

`show etherchannel summary`

<img width="830" height="714" alt="show etherchannel summary" src="https://github.com/user-attachments/assets/ad4defb3-f65b-4b01-9ea1-f951e27d3bdb" />

`show ip route`

<img width="837" height="719" alt="show ip route" src="https://github.com/user-attachments/assets/ed6733f5-02e3-45e8-916f-11733b8b310e" />

### Testes de Conectividade e Segurança (ACL)

Comunicação permitida (VLAN 10 → VLAN 30):

<img width="797" height="745" alt="Comunicação permitida VLAN 10 para VLAN 30" src="https://github.com/user-attachments/assets/3ff2fc6f-3722-4982-b40b-b6703972af09" />

Isolamento de dados sensíveis por ACL (VLAN 40 → VLAN 30):

<img width="740" height="687" alt="Isolamento por ACL VLAN 40 para VLAN 30" src="https://github.com/user-attachments/assets/c33c84ab-75ff-4a2a-9528-5433a234a776" />

## Guia Passo a Passo para Execução dos Testes

1. Baixe o arquivo `.pkt` contido neste repositório e abra no Cisco Packet Tracer.
2. Aguarde a convergência dos protocolos (todas as luzes verdes nos cabos).
3. Abra qualquer estação final (PC ou Laptop) e mude a configuração de IP para DHCP. Confirme o recebimento do IP dinâmico da respectiva VLAN.
4. Para validar o roteamento, abra o Command Prompt em um PC da VLAN 10 e execute `ping 192.168.30.100`.
5. Para validar a ACL de segurança, abra o Command Prompt em um PC da VLAN 40 e execute `ping 192.168.30.100` (o tráfego deve ser bloqueado).

## Conclusão

O projeto demonstra a implementação de uma infraestrutura LAN corporativa segmentada por VLANs, com roteamento Inter-VLAN, agregação de links via LACP, distribuição dinâmica de endereços por DHCP e aplicação de ACLs para controle do tráfego entre departamentos. Os testes realizados no Cisco Packet Tracer comprovam o funcionamento dos principais serviços e mecanismos de segurança da rede.
