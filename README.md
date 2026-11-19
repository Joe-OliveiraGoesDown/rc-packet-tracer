# Redes de Computadores: Subnetting, NAT, VLANs e IPv6 em Packet Tracer

Trabalho de grupo de **Redes de Computadores** (LESI, IPCA, dezembro de 2024), feito no Cisco Packet Tracer, e ainda alguns laboratórios das aulas.

O trabalho simula a rede de três escolas (ESG, EST e ESD), em três partes:

**Grupo I: Subnetting e NAT**
- Esquema de endereçamento **CIDR/VLSM** a partir de `192.168.41.0/24` (93, 50 e 7 hosts)
- Topologia com ISP e 3 routers, e **tabelas de encaminhamento estático**
- Testes de conectividade (`ping`) e `traceroute` entre as sub-redes mais afastadas
- **NAPT** para dar acesso à internet, com análise dos datagramas e da tabela de traduções
- Inventário completo dos equipamentos (interfaces, MAC, IP, máscaras)

**Grupo II: VLANs**
- Endereçamento e segmentação da rede com VLANs

**Grupo III: IPv6**
- Estrutura e tipos de endereços IPv6
- Esquema de endereçamento IPv6 para as três escolas

## Ficheiros

| Ficheiro | Conteúdo |
| --- | --- |
| [`docs/relatorio.pdf`](docs/relatorio.pdf) | Relatório do trabalho (27 páginas) |
| `nat.pkt` | Grupo I: subnetting, encaminhamento estático e NAT |
| `trabalho-vlans.pkt` | Grupo II: VLANs |
| `trabalho-ipv6.pkt` | Grupo III: IPv6 |
| `vlans.pkt` | Laboratório das aulas: VLANs |
| `encaminhamento-estatico.pkt` | Laboratório das aulas: encaminhamento estático |
| `encaminhamento-rip.pkt` | Laboratório das aulas: encaminhamento dinâmico com RIP |

Os ficheiros `.pkt` abrem-se no [Cisco Packet Tracer](https://www.netacad.com/cisco-packet-tracer), que é gratuito com uma conta NetAcad.

## Correções ao relatório (revisão de 2026)

O relatório e os ficheiros `.pkt` estão como foram entregues. Ao rever o trabalho com o enunciado encontrei estes erros. Os valores corretos são:

**Grupo I: encaminhamento estático**

| Router | Destino | Gateway no relatório | Gateway correto |
| --- | --- | --- | --- |
| R3 | 192.168.41.128/26 (EST) | 192.168.2.2 (o próprio R3) | **192.168.2.1** (R1) |
| R2 e R3 | 0.0.0.0/0 (exterior) | não indicada | **rota por omissão para o R1** (192.168.1.1 no R2 e 192.168.2.1 no R3) |
| R1 | 0.0.0.0/0 (exterior) | não indicada | **rota por omissão para o ISP** (70.15.15.1) |

**Grupo II: VLANs.** As máscaras calculadas (/28) estão certas, mas na simulação foi usada `255.0.0.0`. Com /8, as três redes 10.0.0.0, 10.0.1.0 e 10.0.2.0 sobrepõem-se e as SVIs do switch multilayer entram em conflito. A configuração correta é:

| VLAN | Rede | SVI (gateway) | Máscara |
| --- | --- | --- | --- |
| 10 EST | 10.0.0.0/28 | 10.0.0.1 | 255.255.255.240 |
| 20 ESG | 10.0.1.0/28 | 10.0.1.1 | 255.255.255.240 |
| 30 ESD | 10.0.2.0/28 | 10.0.2.1 | 255.255.255.240 |

**Grupo III: IPv6.** As sub-redes deviam começar nos 2 últimos dígitos do número mais baixo: 16941 dá 41, que em hexadecimal é 0x29. O endereçamento correto é:

| Rede | Relatório | Correto |
| --- | --- | --- |
| EST | 2001:a:b:cc01::/64 | **2001:a:b:cc29::/64** |
| ESG | 2001:a:b:cc02::/64 | **2001:a:b:cc2a::/64** |
| ESD | 2001:a:b:cc03::/64 | **2001:a:b:cc2b::/64** |

Faltam também no relatório os pontos 7.1 a 7.5 (endereçamento estático na EST, SLAAC/EUI-64 na ESG, RIPng, tabelas de encaminhamento e testes ICMPv6) e o teste de conectividade entre VLANs (5.6).

## Tecnologias

Cisco Packet Tracer · CIDR/VLSM · encaminhamento estático e RIP · NAT/NAPT · VLANs / 802.1Q · IPv6

## Grupo "Red Ninjas"

| Número | Nome |
| --- | --- |
| 16941 | José Oliveira |
| 26593 | João Soares |
| 31026 | Edgar Casal |
| 31027 | Fernando Coelho |
| 31510 | Simão Machado |
