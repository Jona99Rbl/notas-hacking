### Descripción
We made a lot of substitutions to encrypt this. Can you decrypt it? Connect with `nc jupiter.challenges.picoctf.org 39894`.
### Solución
Iniciamos conectándonos al servidor que nos proporciona la descripción del reto, donde nos proporciona el siguiente mensaje:

```shell
┌──(kali㉿kali)-[~/notas-hacking/crypto_1]
└─$ nc jupiter.challenges.picoctf.org 39894
-------------------------------------------------------------------------------
pshqoimv wtot cv xslo dgiq - dotalthpx_cv_p_snto_gijfei_iqdgpqmxlt
-------------------------------------------------------------------------------
winchq wie vsjt mcjt im jx ecvusvig zwth ch gshesh, c wie ncvcmte mwt focmcvw jlvtlj, ihe jiet vtiopw ijshq mwt fssbv ihe jiuv ch mwt gcfoiox otqioechq moihvxgnihci; cm wie vmolpb jt mwim vsjt dsotbhszgteqt sd mwt pslhmox pslge wioegx dicg ms wint vsjt cjusomihpt ch etigchq zcmw i hsfgtjih sd mwim pslhmox. c dche mwim mwt ecvmocpm wt hijte cv ch mwt trmotjt tivm sd mwt pslhmox, klvm sh mwt fsoetov sd mwott vmimtv, moihvxgnihci, jsgeinci ihe flbsnchi, ch mwt jcevm sd mwt piouimwcih jslhmichv; sht sd mwt zcgetvm ihe gtivm bhszh usomcshv sd tlosut. c ziv hsm ifgt ms gcqwm sh ihx jiu so zsob qcnchq mwt tripm gspigcmx sd mwt pivmgt eoiplgi, iv mwtot iot hs jiuv sd mwcv pslhmox iv xtm ms psjuiot zcmw slo szh soehihpt vlontx jiuv; flm c dslhe mwim fcvmocmy, mwt usvm mszh hijte fx pslhm eoiplgi, cv i dicogx ztgg-bhszh ugipt. c vwigg thmto wtot vsjt sd jx hsmtv, iv mwtx jix otdotvw jx jtjsox zwth c migb snto jx mointgv zcmw jchi.
```

Como se puede apreciar, el mensaje viene codificado, lo cual nos hace investigar sobre el método con el que fue cifrado, después de hacer la búsqueda en internet, nos encontramos con que es por sustitución, siendo un método de cifrado por el que unidades de texto plano son sustituidas con texto cifrado siguiendo un sistema regular; las "unidades" pueden ser una sola letra (el caso más común), pares de letras, tríos de letras, mezclas de lo anterior, entre otros. 

Una vez que sabemos eso, procedemos a buscar una herramienta que nos ayude a resolverlo, encontrando a un solucionador de substitución, donde vamos a tener lo siguiente:

```
Input > -------------------------------------------------------------------------------
pshqoimv wtot cv xslo dgiq - dotalthpx_cv_p_snto_gijfei_iqdgpqmxlt
-------------------------------------------------------------------------------
winchq wie vsjt mcjt im jx ecvusvig zwth ch gshesh, c wie ncvcmte mwt focmcvw jlvtlj, ihe jiet vtiopw ijshq mwt fssbv ihe jiuv ch mwt gcfoiox otqioechq moihvxgnihci; cm wie vmolpb jt mwim vsjt dsotbhszgteqt sd mwt pslhmox pslge wioegx dicg ms wint vsjt cjusomihpt ch etigchq zcmw i hsfgtjih sd mwim pslhmox. c dche mwim mwt ecvmocpm wt hijte cv ch mwt trmotjt tivm sd mwt pslhmox, klvm sh mwt fsoetov sd mwott vmimtv, moihvxgnihci, jsgeinci ihe flbsnchi, ch mwt jcevm sd mwt piouimwcih jslhmichv; sht sd mwt zcgetvm ihe gtivm bhszh usomcshv sd tlosut. c ziv hsm ifgt ms gcqwm sh ihx jiu so zsob qcnchq mwt tripm gspigcmx sd mwt pivmgt eoiplgi, iv mwtot iot hs jiuv sd mwcv pslhmox iv xtm ms psjuiot zcmw slo szh soehihpt vlontx jiuv; flm c dslhe mwim fcvmocmy, mwt usvm mszh hijte fx pslhm eoiplgi, cv i dicogx ztgg-bhszh ugipt. c vwigg thmto wtot vsjt sd jx hsmtv, iv mwtx jix otdotvw jx jtjsox zwth c migb snto jx mointgv zcmw jchi.

Language > English

Output > -------------------------------------------------------------------------------
congrats here is your flag - frequency_is_c_over_lambda_agflcgtyue
-------------------------------------------------------------------------------
having had some time at my disposal when in london, i had visited the british museum, and made search among the books and maps in the library regarding transylvania; it had struck me that some foreknowledge of the country could hardly fail to have some importance in dealing with a nobleman of that country. i find that the district he named is in the extreme east of the country, just on the borders of three states, transylvania, moldavia and bukovina, in the midst of the carpathian mountains; one of the wildest and least known portions of europe. i was not able to light on any map or work giving the exact locality of the castle dracula, as there are no maps of this country as yet to compare with our own ordnance survey maps; but i found that bistritz, the post town named by count dracula, is a fairly well-known place. i shall enter here some of my notes, as they may refresh my memory when i talk over my travels with mina.
```

Dándonos así la bandera que da solución al reto, que como se verá rompe con el formato común con el cual se han encontrado las demás banderas:

```
frequency_is_c_over_lambda_agflcgtyue
```
### Notas Adicionales

### Referencias
https://es.wikipedia.org/wiki/Cifrado_por_sustituci%C3%B3n
https://www.guballa.de/substitution-solver