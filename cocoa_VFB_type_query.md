Query to get neuprint types per id:
pdb.virtualflybrain.org 
```cypher
MATCH (:Site {short_form:'neuprint_JRC_Hemibrain_1point1'})<-[sr:database_cross_reference]-(:Individual)-[:INSTANCEOF]->(c:Class) RETURN sr.accession[0] as id, coalesce(c.symbol[0],c.label) as type
```
example results:
| id           | type                                                                                          |
|--------------|-----------------------------------------------------------------------------------------------|
| "1792802765" | "ORN_DM2"                                                                                     |
| "1041446765" | "adult fan-shaped body layer 6 neuron of DM6 lineage"                                         |
| "794946803"  | "FS"                                                                                          |
| "2042740780" | "ORN_VC4"                                                                                     |
| "915964590"  | "adult fan-shaped body layer 6 neuron of CP2 lineage"                                         |
| "1141687352" | "KCg-m"                                                                                       |
| "1141687352" | "mushroom body dopaminergic neuron"                                                           |
| "1141687352" | "adult dopaminergic neuron"                                                                   |
| "791017605"  | "CL340"                                                                                       |
| "5813089487" | "adult neuron"                                                                                |
| "885599283"  | "FS"                                                                                          |
| "1670390647" | "ORN_DA2"                                                                                     |
| "1110307501" | "PAM08"                                                                                       |
| "1218728544" | "protocerebral bridge glomerulus 9-fan-shaped body-nodulus 3 posterior domain neuron"         |
| "5813054716" | "cholinergic local interneuron of the adult antennal lobe"                                    |
| "5813054716" | "TC-LN"                                                                                       |
| "1702301737" | "ORN_DL3"                                                                                     |
| "922988906"  | "PS008"                                                                                       |
| "1440252127" | "adult glutamatergic neuron"                                                                  |
| "1440252127" | "LT"                                                                                          |
| "641563387"  | "AVLP574"                                                                                     |
| "5813067721" | "MBON14"                                                                                      |
| "538282782"  | "alpha/beta Kenyon cell"                                                                      |
| "538282782"  | "mushroom body dopaminergic neuron"                                                           |
| "538282782"  | "adult dopaminergic neuron"                                                                   |
| "670353202"  | "IB050"                                                                                       |
| "356467849"  | "LHPD3a1"                                                                                     |
| "1808965929" | "LPC1"                                                                                        |
| "1813900946" | "adult cholinergic neuron"                                                                    |
| "1813900946" | "SAD058"                                                                                      |
| "328278368"  | "SMP486"                                                                                      |
| "1168815348" | "LC6"                                                                                         |
| "1685529876" | "MC62"                                                                                        |
| "5812980615" | "adult dopaminergic neuron"                                                                   |
| "5812980615" | "mushroom body dopaminergic neuron"                                                           |
| "5812980615" | "alpha/beta Kenyon cell"                                                                      |
| "884123412"  | "SMP280"                                                                                      |
| "1419162874" | "AVLP558"                                                                                     |
| "357569231"  | "FS"                                                                                          |
| "1047779784" | "LC10"                                                                                        |
| "1047779784" | "adult glutamatergic neuron"                                                                  |
| "2228250473" | "ORN_VM4"                                                                                     |
| "328213594"  | "SLP405"                                                                                      |
| "1480170126" | "AVLP105"                                                                                     |
| "1286315478" | "FB2B"                                                                                        |
| "643398197"  | "IB011"                                                                                       |
| "1567728102" | "protocerebral bridge glomerulus 8-fan-shaped body-nodulus 3 posterior domain neuron"         |
| "5812980579" | "mushroom body dopaminergic neuron"                                                           |
| "5812980579" | "adult dopaminergic neuron"                                                                   |
| "5812980579" | "KCg-m"                                                                                       |
| "821617263"  | "LHPV4d7"                                                                                     |
| "1189887646" | "protocerebral bridge glomerulus 8-fan-shaped body-nodulus 3 posterior domain neuron"         |
| "394064790"  | "adult dopaminergic neuron"                                                                   |
| "394064790"  | "mushroom body dopaminergic neuron"                                                           |
| "394064790"  | "alpha/beta Kenyon cell"                                                                      |
| "5813002722" | "HBeyelet"                                                                                    |
| "5813002722" | "adult GABAergic neuron"                                                                      |
| "1158536635" | "adult cholinergic neuron"                                                                    |
| "1158536635" | "LC18"                                                                                        |
| "329906396"  | "LHAD3a8"                                                                                     |
| "1282693736" | "LC24"                                                                                        |
| "1282693736" | "adult glutamatergic neuron"                                                                  |
| "330388864"  | "adult neurosecretory cell of pars intercerebralis"                                           |
| "1078525257" | "mushroom body dopaminergic neuron"                                                           |
| "1078525257" | "adult dopaminergic neuron"                                                                   |
| "1078525257" | "alpha/beta Kenyon cell"                                                                      |
| "1441499171" | "protocerebral bridge glomerulus 6-fan-shaped body-nodulus 3 posterior domain neuron"         |
| "1537807327" | "AVLP311"                                                                                     |
| "1537807327" | "adult cholinergic neuron"                                                                    |
| "985131499"  | "MBON22"                                                                                      |
| "985131499"  | "adult cholinergic neuron"                                                                    |
| "1698002425" | "ORN_DM1"                                                                                     |
| "1698002425" | "adult cholinergic neuron"                                                                    |
| "5812983658" | "mushroom body dopaminergic neuron"                                                           |
| "5812983658" | "KCg-m"                                                                                       |
| "5812983658" | "adult dopaminergic neuron"                                                                   |
| "5812983346" | "mushroom body dopaminergic neuron"                                                           |
| "5812983346" | "alpha/beta Kenyon cell"                                                                      |
| "5812983346" | "adult dopaminergic neuron"                                                                   |
| "2229230439" | "ORN_VL1"                                                                                     |
| "1378251040" | "PLP211"                                                                                      |
| "418969927"  | "CL182"                                                                                       |
| "1226797688" | "LC"                                                                                          |
| "788427061"  | "FR1"                                                                                         |
| "788427061"  | "adult GABAergic neuron"                                                                      |
| "5813062698" | "PLP249"                                                                                      |
| "1670295588" | "ORN_DM3"                                                                                     |
| "1259377325" | "ER6"                                                                                         |
| "5812983903" | "adult dopaminergic neuron"                                                                   |
| "5812983903" | "KCa'b'-ap1"                                                                                  |
| "5812983903" | "mushroom body dopaminergic neuron"                                                           |
| "1503922566" | "protocerebral bridge glomerulus 4-fan-shaped body-nodulus 3 posterior domain neuron"         |
| "2010992546" | "VM5v_adPN"                                                                                   |
| "988909130"  | "adult fan-shaped body layer 5 neuron of DALcl2 lineage"                                      |
| "988909130"  | "adult glutamatergic neuron"                                                                  |
| "5812986875" | "MC61"                                                                                        |
| "5813060361" | "ORN_VM5d"                                                                                    |
| "5813054697" | "VA1v_adPN"                                                                                   |
| "1670256369" | "ORN_DL1"                                                                                     |
| "1722333743" | "LC18"                                                                                        |
| "1722333743" | "adult cholinergic neuron"                                                                    |
| "734491001"  | "SMP592"                                                                                      |
| "450617762"  | "SLP223"                                                                                      |
| "5901118375" | "CL273"                                                                                       |
| "1533783144" | "adult GABAergic neuron"                                                                      |
| "1533783144" | "AOTU049"                                                                                     |
| "1775638620" | "PS237"                                                                                       |
| "642651049"  | "SIP074"                                                                                      |
| "642651049"  | "adult cholinergic neuron"                                                                    |
| "635424442"  | "LHPV6i1"                                                                                     |
| "5812996881" | "ORN_DL3"                                                                                     |
| "5812981706" | "adult dopaminergic neuron"                                                                   |
| "5812981706" | "mushroom body dopaminergic neuron"                                                           |
| "5812981706" | "KCg-m"                                                                                       |
| "1420306364" | "alpha/beta Kenyon cell"                                                                      |
| "1420306364" | "mushroom body dopaminergic neuron"                                                           |
| "1420306364" | "adult dopaminergic neuron"                                                                   |
| "1660681222" | "VES023"                                                                                      |
| "757215581"  | "LHPV4c1"                                                                                     |
| "484402369"  | "SLP179"                                                                                      |
| "363034407"  | "mushroom body dopaminergic neuron"                                                           |
| "363034407"  | "adult dopaminergic neuron"                                                                   |
| "363034407"  | "alpha/beta Kenyon cell"                                                                      |
| "733700589"  | "SLP283"                                                                                      |
| "1349114660" | "protocerebral bridge glomerulus 4-fan-shaped body-nodulus 3 posterior domain neuron"         |
| "484368420"  | "SLP461"                                                                                      |
| "484368420"  | "adult cholinergic neuron"                                                                    |
| "1314216624" | "PLP143"                                                                                      |
| "1610530558" | "adult serotonergic neuron"                                                                   |
| "1610530558" | "lLN1"                                                                                        |
| "1609883139" | "ORN_DL3"                                                                                     |
| "737150041"  | "KCa'b'-ap2"                                                                                  |
| "737150041"  | "mushroom body dopaminergic neuron"                                                           |
| "737150041"  | "adult dopaminergic neuron"                                                                   |
| "5813024803" | "LLPC"                                                                                        |
| "1080519686" | "adult glutamatergic neuron"                                                                  |
| "1080519686" | "LC10"                                                                                        |
| "574374051"  | "VA5_lPN"                                                                                     |
| "693837780"  | "mushroom body dopaminergic neuron"                                                           |
| "693837780"  | "KCg-m"                                                                                       |
| "693837780"  | "adult dopaminergic neuron"                                                                   |
| "5812981543" | "MBON17"                                                                                      |
| "2006926086" | "VES043"                                                                                      |
| "5813047527" | "ORN_DL2d"                                                                                    |
| "5813047527" | "adult cholinergic neuron"                                                                    |
| "1764445682" | "ORN_DM6"                                                                                     |
| "1764445682" | "adult serotonergic neuron"                                                                   |
| "420567894"  | "SLP088"                                                                                      |
| "420567894"  | "adult glutamatergic neuron"                                                                  |
| "889531496"  | "adult glutamatergic neuron"                                                                  |
| "889531496"  | "PVLP004"                                                                                     |
| "5812979459" | "ER3p"                                                                                        |
| "1100404634" | "DNp26"                                                                                       |
| "1983373284" | "ORN_VA6"                                                                                     |
| "673047760"  | "CRE089"                                                                                      |
| "673047760"  | "adult cholinergic neuron"                                                                    |
| "299043307"  | "SLP218"                                                                                      |
| "1718308979" | "LPLC4"                                                                                       |
| "1718308979" | "adult cholinergic neuron"                                                                    |
| "1067616484" | "CL353"                                                                                       |
| "1559784763" | "adult glutamatergic neuron"                                                                  |
| "1559784763" | "PS282"                                                                                       |
| "613066879"  | "adult cholinergic neuron"                                                                    |
| "613066879"  | "SMP113"                                                                                      |
| "1563393697" | "LC12"                                                                                        |
| "1563393697" | "adult GABAergic neuron"                                                                      |

