As we have all NBLAST score precomputed we can do DS-DS neuron matching (in theory). Best DataSets I could think of was HB->old-FAFB:
```cypher
MATCH (:Site {short_form:'neuprint_JRC_Hemibrain_1point1'})<-[sr:database_cross_reference]-(i:Individual)-[nb:has_similar_morphology_to]->(i2:Individual)-[sr1:database_cross_reference]->(:Site {short_form:'catmaid_fafb'})
WITH sr.accession[0] as hb_id, i.label as hb_label, nb.NBLAST_score[0] as nblast_score, i2.label as fafb_label, sr1.accession[0] as fafb_id
ORDER BY hb_id, nblast_score DESC
WITH hb_id, hb_label, MAX(nblast_score) as max_nblast_score, collect(fafb_id)[0] as fafb_id, collect(fafb_label)[0] as fafb_label
RETURN hb_id, hb_label, max_nblast_score, fafb_id, fafb_label
ORDER BY max_nblast_score DESC
```
We probably want a cut off on the NBLAST score:
| hb_id         | hb_label                                     | max_nblast_score | fafb_id      | fafb_label                        |
|---------------|----------------------------------------------|------------------|--------------|-----------------------------------|
| 1199496234    | MC61 (FlyEM-HB:1199496234)                   | 0.82             | 11994563     | MeTu_DRA#7 (FAFB:11994563)        |
| 1168120382    | MC61 (FlyEM-HB:1168120382)                   | 0.8              | 11908668     | MeTu_DRA#28 (FAFB:11908668)       |
| 1169151891    | MC61 (FlyEM-HB:1169151891)                   | 0.79             | 11993382     | MeTu_DRA#18 (FAFB:11993382)       |
| 1167429753    | MC61 (FlyEM-HB:1167429753)                   | 0.79             | 11993030     | MeTu_DRA#14 (FAFB:11993030)       |
| 1167295856    | ER4d(ring)_L (FlyEM-HB:1167295856)           | 0.78             | 7014310      | R4d#6 (FAFB:7014310)              |
| 1167295916    | ER4d(ring)_R (FlyEM-HB:1167295916)           | 0.78             | 7014310      | R4d#6 (FAFB:7014310)              |
| 1167982211    | ER4d(ring)_L (FlyEM-HB:1167982211)           | 0.78             | 6353358      | R4d#2 (FAFB:6353358)              |
| 1230026228    | ER4d(ring)_L (FlyEM-HB:1230026228)           | 0.78             | 6353358      | R4d#2 (FAFB:6353358)              |
| 941132434     | EPG(PB08)_R6 (FlyEM-HB:941132434)            | 0.78             | 1274528      | EPG-6L#2 (FAFB:1274528)           |
| 1416900410    | ER4d(ring)_L (FlyEM-HB:1416900410)           | 0.78             | 7014310      | R4d#6 (FAFB:7014310)              |
| 1200868959    | MC61 (FlyEM-HB:1200868959)                   | 0.78             | 11994563     | MeTu_DRA#7 (FAFB:11994563)        |
| 1200873417    | MC61 (FlyEM-HB:1200873417)                   | 0.78             | 11994563     | MeTu_DRA#7 (FAFB:11994563)        |
| 1167632513    | ER4d(ring)_R (FlyEM-HB:1167632513)           | 0.77             | 7014310      | R4d#6 (FAFB:7014310)              |
| 1167645523    | ER4d(ring)_L (FlyEM-HB:1167645523)           | 0.77             | 6353358      | R4d#2 (FAFB:6353358)              |
| 541870397     | EPG(PB08)_L6 (FlyEM-HB:541870397)            | 0.77             | 1274528      | EPG-6L#2 (FAFB:1274528)           |
| 1167295853    | ER4d(ring)_L (FlyEM-HB:1167295853)           | 0.77             | 6353358      | R4d#2 (FAFB:6353358)              |
| 1167295872    | ER4d(ring)_L (FlyEM-HB:1167295872)           | 0.77             | 6353358      | R4d#2 (FAFB:6353358)              |
| 1167304403    | ER4d(ring)_R (FlyEM-HB:1167304403)           | 0.77             | 7014310      | R4d#6 (FAFB:7014310)              |
| 1229965474    | ER4d(ring)_R (FlyEM-HB:1229965474)           | 0.77             | 7014310      | R4d#6 (FAFB:7014310)              |
| 1230026402    | ER4d(ring)_L (FlyEM-HB:1230026402)           | 0.77             | 7014310      | R4d#6 (FAFB:7014310)              |
| 1138458221    | MC61 (FlyEM-HB:1138458221)                   | 0.77             | 15600898     | MeTu_DRA#13 (FAFB:15600898)       |
| 1292846965    | ER4d(ring)_L (FlyEM-HB:1292846965)           | 0.77             | 7014310      | R4d#6 (FAFB:7014310)              |
| 1324145475    | ER4d(ring)_R (FlyEM-HB:1324145475)           | 0.77             | 6353358      | R4d#2 (FAFB:6353358)              |
| 1139831106    | MC61 (FlyEM-HB:1139831106)                   | 0.77             | 11993314     | MeTu_DRA#23 (FAFB:11993314)       |
| 1140176382    | MC61 (FlyEM-HB:1140176382)                   | 0.77             | 15978559     | MeTu#14 (FAFB:15978559)           |
| 663190769     | PEN_a(PB06a)_R6 (FlyEM-HB:663190769)         | 0.77             | 659759       | PEN2-6R#1 (FAFB:659759)           |
| 1167891559    | ER4d(ring)_R (FlyEM-HB:1167891559)           | 0.76             | 6353358      | R4d#2 (FAFB:6353358)              |
| 1168461253    | MC61 (FlyEM-HB:1168461253)                   | 0.76             | 11993030     | MeTu_DRA#14 (FAFB:11993030)       |
| 910438331     | EPG(PB08)_R6 (FlyEM-HB:910438331)            | 0.76             | 1274114      | EPG-6R#1 (FAFB:1274114)           |
| 1200864690    | MC61 (FlyEM-HB:1200864690)                   | 0.76             | 11993352     | MeTu_DRA#22 (FAFB:11993352)       |
| 1261000309    | ER4d(ring)_R (FlyEM-HB:1261000309)           | 0.76             | 7014310      | R4d#6 (FAFB:7014310)              |
| 1261056809    | ER4d(ring)_L (FlyEM-HB:1261056809)           | 0.76             | 6353358      | R4d#2 (FAFB:6353358)              |
| 942491983     | EPG(PB08)_R6 (FlyEM-HB:942491983)            | 0.76             | 1274528      | EPG-6L#2 (FAFB:1274528)           |
| 1167300154    | ER4d(ring)_R (FlyEM-HB:1167300154)           | 0.76             | 6353358      | R4d#2 (FAFB:6353358)              |
| 1167300194    | ER4d(ring)_R (FlyEM-HB:1167300194)           | 0.76             | 7014310      | R4d#6 (FAFB:7014310)              |
| 1513674176    | ER4d(ring)_R (FlyEM-HB:1513674176)           | 0.76             | 7014310      | R4d#6 (FAFB:7014310)              |
| 1140172133    | MC61 (FlyEM-HB:1140172133)                   | 0.76             | 11993314     | MeTu_DRA#23 (FAFB:11993314)       |
| 1140176456    | MC61 (FlyEM-HB:1140176456)                   | 0.76             | 11993314     | MeTu_DRA#23 (FAFB:11993314)       |
| 1140517287    | MC61 (FlyEM-HB:1140517287)                   | 0.76             | 11993314     | MeTu_DRA#23 (FAFB:11993314)       |
| 1197993940    | PEN_b(PB06b)_R6 (FlyEM-HB:1197993940)        | 0.76             | 659759       | PEN2-6R#1 (FAFB:659759)           |
| 1198006801    | ER4d(ring)_L (FlyEM-HB:1198006801)           | 0.76             | 6353358      | R4d#2 (FAFB:6353358)              |
| 1198693217    | ER4d(ring)_R (FlyEM-HB:1198693217)           | 0.76             | 7014310      | R4d#6 (FAFB:7014310)              |
| 1198931241    | ER4d(ring)_R (FlyEM-HB:1198931241)           | 0.76             | 7014310      | R4d#6 (FAFB:7014310)              |
| 1199496235    | MC61 (FlyEM-HB:1199496235)                   | 0.76             | 11993064     | MeTu_DRA#27 (FAFB:11993064)       |
| 1107082199    | MC61 (FlyEM-HB:1107082199)                   | 0.76             | 15616477     | MeTu_DRA#12 (FAFB:15616477)       |
| 1167300055    | ER4d(ring)_L (FlyEM-HB:1167300055)           | 0.75             | 7014310      | R4d#6 (FAFB:7014310)              |
| 1167433982    | MC61 (FlyEM-HB:1167433982)                   | 0.75             | 11993030     | MeTu_DRA#14 (FAFB:11993030)       |
| 785888696     | KCab-c_R (FlyEM-HB:785888696)                | 0.75             | 424541       | KC#500-ab (FAFB:424541)           |
| 819828986     | EPG(PB08)_L5 (FlyEM-HB:819828986)            | 0.75             | 1568214      | EPG-5L#1 (FAFB:1568214)           |
| 1169492912    | MC61 (FlyEM-HB:1169492912)                   | 0.75             | 14864504     | MeTu_DRA#25 (FAFB:14864504)       |
| 912596952     | EL(EQ5)_L (FlyEM-HB:912596952)               | 0.75             | 1568214      | EPG-5L#1 (FAFB:1568214)           |
| 5812979222    | ER4d(ring)_R (FlyEM-HB:5812979222)           | 0.75             | 7014310      | R4d#6 (FAFB:7014310)              |
| 1138453852    | MC61 (FlyEM-HB:1138453852)                   | 0.75             | 15616477     | MeTu_DRA#12 (FAFB:15616477)       |
| 5812980799    | KCab-c_R (FlyEM-HB:5812980799)               | 0.75             | 518757       | KC#550-ab (FAFB:518757)           |
| 5812986565    | MC61 (FlyEM-HB:5812986565)                   | 0.75             | 14864504     | MeTu_DRA#25 (FAFB:14864504)       |
| 5812987252    | MC61 (FlyEM-HB:5812987252)                   | 0.75             | 10820916     | MeTu_DRA#31 (FAFB:10820916)       |
| 5813027103    | EPG(PB08)_R5 (FlyEM-HB:5813027103)           | 0.75             | 4087066      | EPG-5L#3 (FAFB:4087066)           |
| 1170667130    | KCa'b'-ap1_R (FlyEM-HB:1170667130)           | 0.75             | 8877321      | KCa'b'-ap1_L#7 (FAFB:8877321)     |
| 694920753     | EPG(PB08)_R5 (FlyEM-HB:694920753)            | 0.75             | 1568214      | EPG-5L#1 (FAFB:1568214)           |
| 725942718     | EL(EQ5)_R (FlyEM-HB:725942718)               | 0.75             | 1568214      | EPG-5L#1 (FAFB:1568214)           |
| 725951521     | EPG(PB08)_R5 (FlyEM-HB:725951521)            | 0.75             | 1568214      | EPG-5L#1 (FAFB:1568214)           |
| 1200527901    | MC61 (FlyEM-HB:1200527901)                   | 0.74             | 10755131     | MeTu_DRA#32 (FAFB:10755131)       |
| 829572544     | KCab-c_R (FlyEM-HB:829572544)                | 0.74             | 424493       | KC#323-ab (FAFB:424493)           |
| 788794171     | EPG(PB08)_L6 (FlyEM-HB:788794171)            | 0.74             | 1274528      | EPG-6L#2 (FAFB:1274528)           |
| 1138807874    | MC61 (FlyEM-HB:1138807874)                   | 0.74             | 11908743     | MeTu_DRA#24 (FAFB:11908743)       |
| 696362840     | EPG(PB08)_L5 (FlyEM-HB:696362840)            | 0.74             | 1568214      | EPG-5L#1 (FAFB:1568214)           |
| 1198473350    | MC61 (FlyEM-HB:1198473350)                   | 0.74             | 15952007     | MeTu_DRA#9 (FAFB:15952007)        |
| 1110173882    | MC61 (FlyEM-HB:1110173882)                   | 0.74             | 11993030     | MeTu_DRA#14 (FAFB:11993030)       |
| 1139494179    | MC61 (FlyEM-HB:1139494179)                   | 0.74             | 11993030     | MeTu_DRA#14 (FAFB:11993030)       |
| 1139485872    | MC61 (FlyEM-HB:1139485872)                   | 0.73             | 11993352     | MeTu_DRA#22 (FAFB:11993352)       |
| 1139831143    | MC61 (FlyEM-HB:1139831143)                   | 0.73             | 14864504     | MeTu_DRA#25 (FAFB:14864504)       |
| 1139835335    | MC61 (FlyEM-HB:1139835335)                   | 0.73             | 14864504     | MeTu_DRA#25 (FAFB:14864504)       |
| 784844112     | KCab-c_R (FlyEM-HB:784844112)                | 0.73             | 518757       | KC#550-ab (FAFB:518757)           |
| 1201210044    | MC61 (FlyEM-HB:1201210044)                   | 0.73             | 10820916     | MeTu_DRA#31 (FAFB:10820916)       |
| 5812986882    | MC61 (FlyEM-HB:5812986882)                   | 0.73             | 11908668     | MeTu_DRA#28 (FAFB:11908668)       |
| 5812987241    | MC61 (FlyEM-HB:5812987241)                   | 0.73             | 15616477     | MeTu_DRA#12 (FAFB:15616477)       |
| 754534424     | DA1_lPN_R (FlyEM-HB:754534424)               | 0.73             | 3239781      | Uniglomerular mALT DA1 lPN#L7 (FAFB:3239781) |
| 754163207     | KCab-c_R (FlyEM-HB:754163207)                | 0.73             | 424541       | KC#500-ab (FAFB:424541)           |
| 798537580     | KCab-c_R (FlyEM-HB:798537580)                | 0.73             | 424541       | KC#500-ab (FAFB:424541)           |
| 1108459090    | MC61 (FlyEM-HB:1108459090)                   | 0.73             | 15616477     | MeTu_DRA#12 (FAFB:15616477)       |
| 1016122913    | KCab-c_R (FlyEM-HB:1016122913)               | 0.73             | 518757       | KC#550-ab (FAFB:518757)           |
| 847254513     | KCab-c_R (FlyEM-HB:847254513)                | 0.73             | 424541       | KC#500-ab (FAFB:424541)           |
| 847336755     | PEN_a(PB06a)_R6 (FlyEM-HB:847336755)         | 0.73             | 3286828      | PEN2-6L#1 (FAFB:3286828)          |
| 879183317     | PEN_b(PB06b)_L6 (FlyEM-HB:879183317)         | 0.73             | 659759       | PEN2-6R#1 (FAFB:659759)           |
| 880875736     | Delta7(PB15)_L5R4_L (FlyEM-HB:880875736)     | 0.73             | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 1167429704    | MC61 (FlyEM-HB:1167429704)                   | 0.73             | 15749047     | MeTu_DRA#5 (FAFB:15749047)        |
| 910801332     | Delta7(PB15)_L5R4_L (FlyEM-HB:910801332)     | 0.73             | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 912601268     | EPG(PB08)_L6 (FlyEM-HB:912601268)            | 0.73             | 1274528      | EPG-6L#2 (FAFB:1274528)           |
| 5812980803    | KCab-c_R (FlyEM-HB:5812980803)               | 0.73             | 518757       | KC#550-ab (FAFB:518757)           |
| 5813021446    | KCab-c_R (FlyEM-HB:5813021446)               | 0.73             | 518757       | KC#550-ab (FAFB:518757)           |
| 5813021805    | KCa'b'-ap1_R (FlyEM-HB:5813021805)           | 0.73             | 8880337      | tKCa'b'-ap1_L#2 (FAFB:8880337)    |
| 1137426370    | MC61 (FlyEM-HB:1137426370)                   | 0.73             | 12127369     | MeTu_DRA#17 (FAFB:12127369)       |
| 1198809663    | MC61 (FlyEM-HB:1198809663)                   | 0.73             | 11994563     | MeTu_DRA#7 (FAFB:11994563)        |
| 1199150719    | MC61 (FlyEM-HB:1199150719)                   | 0.73             | 11993382     | MeTu_DRA#18 (FAFB:11993382)       |
| 425790257     | APL_R (FlyEM-HB:425790257)                   | 0.73             | 203840       | APL 203841 MR JSL (FAFB:203840)   |
| 693453332     | KCab-c_R (FlyEM-HB:693453332)                | 0.73             | 518757       | KC#550-ab (FAFB:518757)           |
| 846611908     | KCab-c_R (FlyEM-HB:846611908)                | 0.72             | 10598        | KC#90-ab (FAFB:10598)             |
| 847254566     | KCab-c_R (FlyEM-HB:847254566)                | 0.72             | 424541       | KC#500-ab (FAFB:424541)           |
| 847595624     | KCab-c_R (FlyEM-HB:847595624)                | 0.72             | 518757       | KC#550-ab (FAFB:518757)           |
| 1107423158    | MC61 (FlyEM-HB:1107423158)                   | 0.72             | 15616477     | MeTu_DRA#12 (FAFB:15616477)       |
| 1108450770    | MC61 (FlyEM-HB:1108450770)                   | 0.72             | 15600898     | MeTu_DRA#13 (FAFB:15600898)       |
| 1199837203    | MC61 (FlyEM-HB:1199837203)                   | 0.72             | 15749075     | MeTu_DRA#30 (FAFB:15749075)       |
| 789126240     | EPG(PB08)_L5 (FlyEM-HB:789126240)            | 0.72             | 4087066      | EPG-5L#3 (FAFB:4087066)           |
| 798537538     | KCab-c_R (FlyEM-HB:798537538)                | 0.72             | 518757       | KC#550-ab (FAFB:518757)           |
| 5812986257    | MC64 (FlyEM-HB:5812986257)                   | 0.72             | 11908710     | MeTu_DRA#3 (FAFB:11908710)        |
| 923013923     | KCab-c_R (FlyEM-HB:923013923)                | 0.72             | 518757       | KC#550-ab (FAFB:518757)           |
| 1889883818    | VL2a_vPN_R (FlyEM-HB:1889883818)             | 0.72             | 1724523      | Uniglomerular mlALT VL2a vPN#R3 (FAFB:1724523) |
| 829568160     | KCab-c_R (FlyEM-HB:829568160)                | 0.72             | 424541       | KC#500-ab (FAFB:424541)           |
| 1036753721    | EL(EQ5)_L (FlyEM-HB:1036753721)              | 0.72             | 1274528      | EPG-6L#2 (FAFB:1274528)           |
| 5812981858    | KCa'b'-ap1_R (FlyEM-HB:5812981858)           | 0.72             | 5832021      | KCa'b'-ap1_R#5 (FAFB:5832021)     |
| 5812981970    | KCab-c_R (FlyEM-HB:5812981970)               | 0.72             | 518757       | KC#550-ab (FAFB:518757)           |
| 5812982520    | KCab-c_R (FlyEM-HB:5812982520)               | 0.72             | 518757       | KC#550-ab (FAFB:518757)           |
| 5812982803    | KCg-m_R (FlyEM-HB:5812982803)                | 0.72             | 8369584      | KC#670-y (FAFB:8369584)           |
| 910796989     | Delta7(PB15)_L5R4_L (FlyEM-HB:910796989)     | 0.72             | 676155       | Delta7-5R4L#2 (FAFB:676155)       |
| 5813020138    | WEDPN3_R (FlyEM-HB:5813020138)               | 0.72             | 1313334      | WEDPN3#3 (FAFB:1313334)           |
| 2286836128    | JO-A/B/C (FlyEM-HB:2286836128)               | 0.72             | 3652095      | JO-B-19 (type-2) (FAFB:3652095)   |
| 5813021023    | KCab-c_R (FlyEM-HB:5813021023)               | 0.72             | 533321       | KC#552-ab (FAFB:533321)           |
| 1640909284    | lLN2F_b(Full)_R (FlyEM-HB:1640909284)        | 0.72             | 829827       | Dense ABAF LN#1 (FAFB:829827)     |
| 332003899     | KCab-c_R (FlyEM-HB:332003899)                | 0.72             | 424493       | KC#323-ab (FAFB:424493)           |
| 5813066705    | JO-A/B/C (FlyEM-HB:5813066705)               | 0.72             | 3652095      | JO-B-19 (type-2) (FAFB:3652095)   |
| 1198809657    | MC61 (FlyEM-HB:1198809657)                   | 0.72             | 11992932     | MeTu_DRA#19 (FAFB:11992932)       |
| 394755632     | KCab-c_R (FlyEM-HB:394755632)                | 0.72             | 424541       | KC#500-ab (FAFB:424541)           |
| 394755645     | KCab-c_R (FlyEM-HB:394755645)                | 0.72             | 518757       | KC#550-ab (FAFB:518757)           |
| 457196444     | MBON18(a2sc)(PDL05)_L (FlyEM-HB:457196444)   | 0.72             | 2062703      | MBON-a2sp_R (FAFB:2062703)        |
| 5812987715    | MC61 (FlyEM-HB:5812987715)                   | 0.71             | 12127369     | MeTu_DRA#17 (FAFB:12127369)       |
| 693116396     | KCab-c_R (FlyEM-HB:693116396)                | 0.71             | 518757       | KC#550-ab (FAFB:518757)           |
| 693448777     | KCab-c_R (FlyEM-HB:693448777)                | 0.71             | 518757       | KC#550-ab (FAFB:518757)           |
| 734581598     | Delta7(PB15)_L6R3_L (FlyEM-HB:734581598)     | 0.71             | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 769721865     | KCab-c_R (FlyEM-HB:769721865)                | 0.71             | 424541       | KC#500-ab (FAFB:424541)           |
| 1139490024    | MC61 (FlyEM-HB:1139490024)                   | 0.71             | 11992932     | MeTu_DRA#19 (FAFB:11992932)       |
| 1168120360    | MC61 (FlyEM-HB:1168120360)                   | 0.71             | 11992932     | MeTu_DRA#19 (FAFB:11992932)       |
| 754538881     | DA1_lPN_R (FlyEM-HB:754538881)               | 0.71             | 2380564      | Uniglomerular mALT DA1 lPN#L5 (FAFB:2380564) |
| 725951660     | EL(EQ5)_R (FlyEM-HB:725951660)               | 0.71             | 1274114      | EPG-6R#1 (FAFB:1274114)           |
| 664645558     | PEN_a(PB06a)_L6 (FlyEM-HB:664645558)         | 0.71             | 607812       | PEN1-6R#2 (FAFB:607812)           |
| 979519562     | LHAV4c1_a_R (FlyEM-HB:979519562)             | 0.71             | 1853423      | LHAV4a4#2 (FAFB:1853423)          |
| 784844007     | KCab-c_R (FlyEM-HB:784844007)                | 0.71             | 424541       | KC#500-ab (FAFB:424541)           |
| 784882707     | KCab-c_R (FlyEM-HB:784882707)                | 0.71             | 10598        | KC#90-ab (FAFB:10598)             |
| 816219622     | KCab-c_R (FlyEM-HB:816219622)                | 0.71             | 518757       | KC#550-ab (FAFB:518757)           |
| 824353701     | VL2p_vPN_R (FlyEM-HB:824353701)              | 0.71             | 4507894      | Uniglomerular mlALT VL2p vPN#L1 (FAFB:4507894) |
| 5812982204    | KCab-c_R (FlyEM-HB:5812982204)               | 0.71             | 424421       | KC#315-ab (FAFB:424421)           |
| 911129339     | Delta7(PB15)_L4R5_R (FlyEM-HB:911129339)     | 0.71             | 676155       | Delta7-5R4L#2 (FAFB:676155)       |
| 911211196     | Delta7(PB15)_L6R4_L (FlyEM-HB:911211196)     | 0.71             | 676155       | Delta7-5R4L#2 (FAFB:676155)       |
| 911578595     | Delta7(PB15)_L8R1R9_L (FlyEM-HB:911578595)   | 0.71             | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 911919044     | Delta7(PB15)_L6R3_L (FlyEM-HB:911919044)     | 0.71             | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 5812981965    | KCab-c_R (FlyEM-HB:5812981965)               | 0.71             | 518757       | KC#550-ab (FAFB:518757)           |
| 880530613     | Delta7(PB15)_L5R4_L (FlyEM-HB:880530613)     | 0.71             | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 881898734     | PEG(PB07)_L6 (FlyEM-HB:881898734)            | 0.71             | 963438       | PEG-6L (FAFB:963438)              |
| 1640922516    | lLN2T_e(Tortuous)_R (FlyEM-HB:1640922516)    | 0.71             | 2891306      | Dense ABAF LN#2 (FAFB:2891306)    |
| 5813058367    | FB6I_L (FlyEM-HB:5813058367)                 | 0.71             | 2416734      | Protocerebral_DAN_input_c 11.14.1#1 (FAFB:2416734) |
| 332003730     | KCab-c_R (FlyEM-HB:332003730)                | 0.71             | 518757       | KC#550-ab (FAFB:518757)           |
| 364066029     | KCab-c_R (FlyEM-HB:364066029)                | 0.71             | 424541       | KC#500-ab (FAFB:424541)           |
| 1171548212    | MC61 (FlyEM-HB:1171548212)                   | 0.71             | 11908710     | MeTu_DRA#3 (FAFB:11908710)        |
| 1380495496    | PEN_a(PB06a)_L6 (FlyEM-HB:1380495496)        | 0.71             | 659759       | PEN2-6R#1 (FAFB:659759)           |
| 1414327340    | MC61 (FlyEM-HB:1414327340)                   | 0.71             | 15616477     | MeTu_DRA#12 (FAFB:15616477)       |
| 669869547     | LHAV4a4_R (FlyEM-HB:669869547)               | 0.71             | 1853423      | LHAV4a4#2 (FAFB:1853423)          |
| 1699974843    | lLN2T_e(Tortuous)_R (FlyEM-HB:1699974843)    | 0.71             | 2891306      | Dense ABAF LN#2 (FAFB:2891306)    |
| 1137085521    | MC61 (FlyEM-HB:1137085521)                   | 0.71             | 14726392     | MeTu#15 (FAFB:14726392)           |
| 1137085624    | MC61 (FlyEM-HB:1137085624)                   | 0.71             | 12127369     | MeTu_DRA#17 (FAFB:12127369)       |
| 1138795022    | MC61 (FlyEM-HB:1138795022)                   | 0.71             | 15600898     | MeTu_DRA#13 (FAFB:15600898)       |
| 1138807923    | MC61 (FlyEM-HB:1138807923)                   | 0.71             | 10755131     | MeTu_DRA#32 (FAFB:10755131)       |
| 5813024698    | lLN2F_b(Full)_R (FlyEM-HB:5813024698)        | 0.71             | 829827       | Dense ABAF LN#1 (FAFB:829827)     |
| 5813027747    | KCab-c_R (FlyEM-HB:5813027747)               | 0.71             | 518757       | KC#550-ab (FAFB:518757)           |
| 980198319     | LHAV4a4_R (FlyEM-HB:980198319)               | 0.7              | 1853423      | LHAV4a4#2 (FAFB:1853423)          |
| 5812983943    | aMe10_L (FlyEM-HB:5812983943)                | 0.7              | 164544       | aMe12#3 (FAFB:164544)             |
| 1734350788    | DA1_lPN_R (FlyEM-HB:1734350788)              | 0.7              | 2380564      | Uniglomerular mALT DA1 lPN#L5 (FAFB:2380564) |
| 487834111     | KCa'b'-ap1_R (FlyEM-HB:487834111)            | 0.7              | 8880337      | tKCa'b'-ap1_L#2 (FAFB:8880337)    |
| 848287126     | KCab-c_R (FlyEM-HB:848287126)                | 0.7              | 10818        | KC#98-ab (FAFB:10818)             |
| 736126563     | KCab-c_R (FlyEM-HB:736126563)                | 0.7              | 518757       | KC#550-ab (FAFB:518757)           |
| 1795440828    | ORN_DC1_R (FlyEM-HB:1795440828)              | 0.7              | 11355584     | DC1 ORN #1 (FAFB:11355584)        |
| 941123755     | PEN_b(PB06b)_R6 (FlyEM-HB:941123755)         | 0.7              | 3286828      | PEN2-6L#1 (FAFB:3286828)          |
| 941482720     | Delta7(PB15)_L6R3_L (FlyEM-HB:941482720)     | 0.7              | 676155       | Delta7-5R4L#2 (FAFB:676155)       |
| 664650297     | PEN_b(PB06b)_L6 (FlyEM-HB:664650297)         | 0.7              | 659759       | PEN2-6R#1 (FAFB:659759)           |
| 574037281     | VA5_lPN_R (FlyEM-HB:574037281)               | 0.7              | 57365        | Uniglomerular mALT VA5 lPN#R1 (FAFB:57365) |
| 574374051     | VA5_lPN_R (FlyEM-HB:574374051)               | 0.7              | 57365        | Uniglomerular mALT VA5 lPN#R1 (FAFB:57365) |
| 1016123127    | KCab-c_R (FlyEM-HB:1016123127)               | 0.7              | 518757       | KC#550-ab (FAFB:518757)           |
| 910386568     | KCab-c_R (FlyEM-HB:910386568)                | 0.7              | 10698        | KC#93-ab (FAFB:10698)             |
| 726207450     | VM4_lvPN_R (FlyEM-HB:726207450)              | 0.7              | 57003        | Uniglomerular mALT VM4 lvPN#R1 (FAFB:57003) |
| 755173189     | KCab-c_R (FlyEM-HB:755173189)                | 0.7              | 518757       | KC#550-ab (FAFB:518757)           |
| 755868550     | KCab-c_R (FlyEM-HB:755868550)                | 0.7              | 424541       | KC#500-ab (FAFB:424541)           |
| 1231554116    | MC61 (FlyEM-HB:1231554116)                   | 0.7              | 10820916     | MeTu_DRA#31 (FAFB:10820916)       |
| 910442752     | Delta7(PB15)_L8R1R9_L (FlyEM-HB:910442752)   | 0.7              | 6454109      | Delta7-2R7L#1 (FAFB:6454109)      |
| 910442782     | Delta7(PB15)_L4R6_R (FlyEM-HB:910442782)     | 0.7              | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 910783883     | Delta7(PB15)_L8R1R9_L (FlyEM-HB:910783883)   | 0.7              | 6454109      | Delta7-2R7L#1 (FAFB:6454109)      |
| 911134009     | Delta7(PB15)_L4R5_R (FlyEM-HB:911134009)     | 0.7              | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 911138168     | Delta7(PB15)_L4R5_R (FlyEM-HB:911138168)     | 0.7              | 3017999      | Delta7-5R4L#1 (FAFB:3017999)      |
| 911400981     | KCab-c_R (FlyEM-HB:911400981)                | 0.7              | 10714        | KC#94-ab (FAFB:10714)             |
| 911901802     | Delta7(PB15)_L4R6_R (FlyEM-HB:911901802)     | 0.7              | 3017999      | Delta7-5R4L#1 (FAFB:3017999)      |
| 911911004     | Delta7(PB15)_L1L9R8_R (FlyEM-HB:911911004)   | 0.7              | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 911911193     | Delta7(PB15)_L8R1R9_L (FlyEM-HB:911911193)   | 0.7              | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 911919917     | Delta7(PB15)_L1L9R8_R (FlyEM-HB:911919917)   | 0.7              | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 912243353     | Delta7(PB15)_L7R2_L (FlyEM-HB:912243353)     | 0.7              | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 5813016455    | aMe10_L (FlyEM-HB:5813016455)                | 0.7              | 164544       | aMe12#3 (FAFB:164544)             |
| 5813020061    | KCa'b'-ap1_R (FlyEM-HB:5813020061)           | 0.7              | 8880337      | tKCa'b'-ap1_L#2 (FAFB:8880337)    |
| 941814787     | Delta7(PB15)_L6R3_L (FlyEM-HB:941814787)     | 0.7              | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 954053251     | KCab-c_R (FlyEM-HB:954053251)                | 0.7              | 424487       | KC#495-ab (FAFB:424487)           |
| 922677093     | KCab-c_R (FlyEM-HB:922677093)                | 0.7              | 424421       | KC#315-ab (FAFB:424421)           |
| 5812981109    | KCab-c_R (FlyEM-HB:5812981109)               | 0.7              | 518757       | KC#550-ab (FAFB:518757)           |
| 2008239574    | HRN_VP4_R (FlyEM-HB:2008239574)              | 0.7              | 12819065     | VP4RNr#11 (FAFB:12819065)         |
| 5812983298    | KCab-c_R (FlyEM-HB:5812983298)               | 0.7              | 424541       | KC#500-ab (FAFB:424541)           |
| 5813014585    | LHAV4a4_R (FlyEM-HB:5813014585)              | 0.7              | 1911124      | LHAV4a4#1 (FAFB:1911124)          |
| 2131372750    | HRN_VP5_R (FlyEM-HB:2131372750)              | 0.7              | 5678610      | VP5RNr#5 (FAFB:5678610)           |
| 1158747783    | Delta7(PB15)_L7R2_L (FlyEM-HB:1158747783)    | 0.7              | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 1167433978    | MC61 (FlyEM-HB:1167433978)                   | 0.7              | 11992932     | MeTu_DRA#19 (FAFB:11992932)       |
| 816219578     | KCab-c_R (FlyEM-HB:816219578)                | 0.7              | 424421       | KC#315-ab (FAFB:424421)           |
| 816219675     | KCab-c_R (FlyEM-HB:816219675)                | 0.7              | 518757       | KC#550-ab (FAFB:518757)           |
| 818637585     | KCab-c_R (FlyEM-HB:818637585)                | 0.7              | 10598        | KC#90-ab (FAFB:10598)             |
| 1138803621    | MC61 (FlyEM-HB:1138803621)                   | 0.7              | 15600898     | MeTu_DRA#13 (FAFB:15600898)       |
| 1138807902    | MC61 (FlyEM-HB:1138807902)                   | 0.7              | 15749075     | MeTu_DRA#30 (FAFB:15749075)       |
| 878324222     | KCab-c_R (FlyEM-HB:878324222)                | 0.7              | 10598        | KC#90-ab (FAFB:10598)             |
| 880880259     | Delta7(PB15)_L4R5_R (FlyEM-HB:880880259)     | 0.7              | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 881221166     | Delta7(PB15)_L1L9R8_R (FlyEM-HB:881221166)   | 0.7              | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 394755376     | KCab-m_R (FlyEM-HB:394755376)                | 0.7              | 518757       | KC#550-ab (FAFB:518757)           |
| 5813039315    | DA1_lPN_R (FlyEM-HB:5813039315)              | 0.7              | 3239781      | Uniglomerular mALT DA1 lPN#L7 (FAFB:3239781) |
| 5813048042    | Delta7(PB15)_L5R4_L (FlyEM-HB:5813048042)    | 0.7              | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 5813061383    | Delta7(PB15)_L1L9R8_R (FlyEM-HB:5813061383)  | 0.7              | 6454109      | Delta7-2R7L#1 (FAFB:6454109)      |
| 1670287030    | lLN2F_a(Full)_R (FlyEM-HB:1670287030)        | 0.7              | 829827       | Dense ABAF LN#1 (FAFB:829827)     |
| 5813091021    | KCa'b'-ap1_R (FlyEM-HB:5813091021)           | 0.7              | 5832021      | KCa'b'-ap1_R#5 (FAFB:5832021)     |
| 5813104106    | MC61 (FlyEM-HB:5813104106)                   | 0.7              | 15952007     | MeTu_DRA#9 (FAFB:15952007)        |
| 5901218894    | lLN2F_a(Full)_R (FlyEM-HB:5901218894)        | 0.7              | 2891306      | Dense ABAF LN#2 (FAFB:2891306)    |
| 603349484     | M_vPNml85_R (FlyEM-HB:603349484)             | 0.7              | 4624362      | Multiglomerular mlALT vPN#R21 (FAFB:4624362) |
| 332003372     | KCab-c_R (FlyEM-HB:332003372)                | 0.7              | 424541       | KC#500-ab (FAFB:424541)           |
| 1170861854    | MC61 (FlyEM-HB:1170861854)                   | 0.7              | 11993352     | MeTu_DRA#22 (FAFB:11993352)       |
| 1442293171    | LC10 (FlyEM-HB:1442293171)                   | 0.7              | 15616477     | MeTu_DRA#12 (FAFB:15616477)       |
| 1451341240    | KCab-c_R (FlyEM-HB:1451341240)               | 0.7              | 424469       | KC#321-ab (FAFB:424469)           |
| 1704347707    | lLN2T_c(Tortuous)_R (FlyEM-HB:1704347707)    | 0.7              | 2891306      | Dense ABAF LN#2 (FAFB:2891306)    |
| 1732313117    | M_lvPNm40_R (FlyEM-HB:1732313117)            | 0.69             | 57039        | Multiglomerular mALT lvPN#R38 (FAFB:57039) |
| 729219639     | M_vPNml74_R (FlyEM-HB:729219639)             | 0.69             | 3813495      | Multiglomerular mlALT vPN#R44 (FAFB:3813495) |
| 846611449     | KCab-c_R (FlyEM-HB:846611449)                | 0.69             | 10818        | KC#98-ab (FAFB:10818)             |
| 847250148     | KCab-c_R (FlyEM-HB:847250148)                | 0.69             | 424541       | KC#500-ab (FAFB:424541)           |
| 767161677     | KCab-m_R (FlyEM-HB:767161677)                | 0.69             | 424541       | KC#500-ab (FAFB:424541)           |
| 760250272     | M_vPNml84_R (FlyEM-HB:760250272)             | 0.69             | 6702019      | Multiglomerular mlALT vPN#R13 (FAFB:6702019) |
| 5813021441    | KCab-m_R (FlyEM-HB:5813021441)               | 0.69             | 518757       | KC#550-ab (FAFB:518757)           |
| 791298858     | M_vPNml84_R (FlyEM-HB:791298858)             | 0.69             | 4632128      | Multiglomerular mlALT vPN#R12 (FAFB:4632128) |
| 730169579     | FB2F_a_L (FlyEM-HB:730169579)                | 0.69             | 1546454      | FB2H#1 (FAFB:1546454)             |
| 692792746     | KCab-c_R (FlyEM-HB:692792746)                | 0.69             | 518757       | KC#550-ab (FAFB:518757)           |
| 1107423142    | MC61 (FlyEM-HB:1107423142)                   | 0.69             | 11455112     | MeTu#6 (FAFB:11455112)            |
| 1108109641    | MC61 (FlyEM-HB:1108109641)                   | 0.69             | 15600898     | MeTu_DRA#13 (FAFB:15600898)       |
| 856407289     | LHAV4a4_R (FlyEM-HB:856407289)               | 0.69             | 1853423      | LHAV4a4#2 (FAFB:1853423)          |
| 1734350908    | DA1_lPN_R (FlyEM-HB:1734350908)              | 0.69             | 3239781      | Uniglomerular mALT DA1 lPN#L7 (FAFB:3239781) |
| 983362172     | AVLP009_R (FlyEM-HB:983362172)               | 0.69             | 6540243      | vpoIN#11 (FAFB:6540243)           |
| 5812989057    | MC61 (FlyEM-HB:5812989057)                   | 0.69             | 10438339     | MeTu_DRA#8 (FAFB:10438339)        |
| 887433630     | LHAV4e2_b_R (FlyEM-HB:887433630)             | 0.69             | 1853423      | LHAV4a4#2 (FAFB:1853423)          |
| 891642176     | KCab-c_R (FlyEM-HB:891642176)                | 0.69             | 424541       | KC#500-ab (FAFB:424541)           |
| 1202250762    | MC61 (FlyEM-HB:1202250762)                   | 0.69             | 11695293     | MeTu_DRA#4 (FAFB:11695293)        |
| 941810314     | Delta7(PB15)_L7R3_L (FlyEM-HB:941810314)     | 0.69             | 676155       | Delta7-5R4L#2 (FAFB:676155)       |
| 798196461     | KCab-c_R (FlyEM-HB:798196461)                | 0.69             | 518757       | KC#550-ab (FAFB:518757)           |
| 753852265     | KCab-c_R (FlyEM-HB:753852265)                | 0.69             | 10598        | KC#90-ab (FAFB:10598)             |
| 1167895489    | ER2_c(ring)_R (FlyEM-HB:1167895489)          | 0.69             | 6813859      | R4d#4 (FAFB:6813859)              |
| 1167896065    | ER2_c(ring)_R (FlyEM-HB:1167896065)          | 0.69             | 6353358      | R4d#2 (FAFB:6353358)              |
| 1140172174    | MC61 (FlyEM-HB:1140172174)                   | 0.69             | 11903992     | MeTu_DRA#29 (FAFB:11903992)       |
| 1140189290    | MC64 (FlyEM-HB:1140189290)                   | 0.69             | 11993352     | MeTu_DRA#22 (FAFB:11993352)       |
| 970777114     | KCab-c_R (FlyEM-HB:970777114)                | 0.69             | 13926        | KC#181-ab (FAFB:13926)            |
| 910783731     | Delta7(PB15)_L8R1R9_L (FlyEM-HB:910783731)   | 0.69             | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 910783961     | Delta7(PB15)_L3R6_R (FlyEM-HB:910783961)     | 0.69             | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 911129204     | Delta7(PB15)_L7R2_L (FlyEM-HB:911129204)     | 0.69             | 6454109      | Delta7-2R7L#1 (FAFB:6454109)      |
| 911241750     | Delta7(PB15)_L6R4_L (FlyEM-HB:911241750)     | 0.69             | 632638       | Delta7-6R3L#1 (FAFB:632638)       |
| 911565419     | Delta7(PB15)_L3R6_R (FlyEM-HB:911565419)     | 0.69             | 3017999      | Delta7-5R4L#1 (FAFB:3017999)      |
| 911574261     | Delta7(PB15)_L1L9R8_R (FlyEM-HB:911574261)   | 0.69             | 6454109      | Delta7-2R7L#1 (FAFB:6454109)      |
| 911578496     | Delta7(PB15)_L2R7_R (FlyEM-HB:911578496)     | 0.69             | 676155       | Delta7-5R4L#2 (FAFB:676155)       |
| 1977545462    | HRN_VP4_R (FlyEM-HB:1977545462)              | 0.69             | 12819065     | VP4RNr#11 (FAFB:12819065)         |
| 1977553534    | HRN_VP4_R (FlyEM-HB:1977553534)              | 0.69             | 12819089     | VP4RNl#7 (FAFB:12819089)          |
| 5812983006    | KCab-c_R (FlyEM-HB:5812983006)               | 0.69             | 424541       | KC#500-ab (FAFB:424541)           |
| 5813016658    | MC61 (FlyEM-HB:5813016658)                   | 0.69             | 15616477     | MeTu_DRA#12 (FAFB:15616477)       |
| 5812982211    | KCab-m_R (FlyEM-HB:5812982211)               | 0.69             | 518757       | KC#550-ab (FAFB:518757)           |
| 1225100939    | VP2+VC5_l2PN(lALT)_R (FlyEM-HB:1225100939)   | 0.69             | 10515783     | VP2+VC5 l2PN_L (FAFB:10515783)    |

