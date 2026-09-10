# Portfólio Prático de Infraestrutura de Redes LAN Corporativas com Simulação em Cisco Packet Tracer  - InovaTech Soluções!
Engenharia &amp; Infraestrutura de Redes | Projeto prático de LAN corporativa com alta disponibilidade (LACP/STP), segmentação por VLANs e roteamento Layer 3 no Cisco Packet Tracer. 🌐⚡

## 👥 Integrantes do Grupo
* [Brenda Sousa Costa]
* [Maria Vitória Pereira dos Santos]
* [Nome do Integrante 3]
* [Nome do Integrante 4]
* [Nome do Integrante 5]
* [Nome do Integrante 6]

---

## 🏢 Cenário da Empresa
A empresa **InovaTech Soluções** modernizou sua infraestrutura de rede local (LAN) para atender à expansão de suas operações. A topologia foi desenvolvida para suportar alta performance local, resiliência, automação de serviços e segurança no controle de tráfego entre departamentos.

---

## 📊 Tabela de Endereçamento IP e VLANs

| Segmento / VLAN | Faixa de IP (Sub-rede) | Gateway Padrão | Escopo / Departamentos |
| :--- | :--- | :--- | :--- |
| **VLAN 10 (Diretoria)** | 192.168.10.0/24 | 192.168.10.1 | Acesso restrito e servidores críticos |
| **VLAN 20 (TI / Infra)** | 192.168.20.0/24 | 192.168.20.1 | Admins de rede e suporte |
| **VLAN 30 (Financeiro)** | 192.168.30.0/24 | 192.168.30.1 | Estações financeiras e banco de dados |
| **VLAN 40 (Atendimento)**| 192.168.40.0/24 | 192.168.40.1 | Suporte operacional ao cliente |

---

## ⚙️ Funcionalidades Implementadas
* **Switches Layer 3:** Roteamento Inter-VLAN ativado no núcleo da rede.
* **Agregação de Links (EtherChannel/LACP):** Links trunk agrupados em alta disponibilidade.
* **Automação DHCP Relay:** Distribuição dinâmica de IPs com apoio de `ip helper-address`.
* **Segurança Perimetral (ACL):** Bloqueio de tráfego originado no Atendimento (VLAN 40) direcionado ao Financeiro (VLAN 30).

---

## 🧪 Guia Passo a Passo para Execução dos Testes

1. Baixe o arquivo `.pkt` contido neste repositório e abra no **Cisco Packet Tracer**.
2. Aguarde a convergência dos protocolos (todas as luzes verdes nos cabos).
3. Abra qualquer estação final (PC ou Laptop) e mude a configuração de IP para **DHCP**. Confirme o recebimento do IP dinâmico da respectiva VLAN.
4. Para validar o roteamento, abra o **Command Prompt** em um PC da VLAN 10 e execute `ping 192.168.30.100`.
5. Para validar a ACL de segurança, abra o **Command Prompt** em um PC da VLAN 40 e execute `ping 192.168.30.100` (o tráfego deve ser bloqueado).
