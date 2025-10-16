# Webservice de consulta de deutes tributaris per a ajuntaments

## Procediment d’adhesió
1. Descarregar el [formulari d'adhesió](https://github.com/organisme-de-gestio-tributaria/consulta-deutes-tributaris/blob/main/Formulari%20d'adhesi%C3%B3.pdf). Si no es visualitza al navegador, descarregueu-lo al vostre dispositiu.
2. Emplenar el formulari.
3. El formulari l'ha de signar la Tresorer/a, Interventor/a o Alcalde/sa.
3. Enviar el formulari signat via EACAT a l’ORGT.

## Informació tècnica

Cal accedir al webservice mitjançat l'endpoint REST. L’especificació es pot obtenir del [fitxer swagger disponible en aquest repositori](https://github.com/organisme-de-gestio-tributaria/consulta-deutes-tributaris/blob/main/swagger%20DeutesTributs.json).

El servei es troba a les següents URL's:
* Producció: https://wsreal.orgt.diba.cat/Deutes/DeutesServiceREST.svc 
* Pre-produció (proves): https://wsproves.orgt.diba.cat/Deutes/DeutesServiceREST.svc

Respecte a la seguretat, cal tenir en compte:
1. L’accés al web service serà via https i amb certificat d'òrgan. 
1. Es comprovarà que les dades enviades corresponen a l’Ajuntament associat al certificat. Per fer les proves també cal fer servir un certificat d'òrgan.
1. **Previ a les proves cal comunicar el certificat utilitzat a l’ORGT ja que és necessari instal·lar la clau pública als servidors de la ORGT.** Vegeu el procés de sol·licitud a la [pàgina principal](https://github.com/organisme-de-gestio-tributaria/organisme-de-gestio-tributaria)

Els endpoints disponibles són:
1. **GenerarDocumentREST** Permet generar els documents acreditatius de que un DNI/NIF té o no té deutes amb l'ajuntament. Cal introduir:
   - CodiINE10: codi INE10 de l'ajuntament
   - DNINIFContribuent: DNI/NIF del contribuent (8 dígits, sense la lletra de control)
   - Idioma: Idioma del document final (C: català o E: castellà)
1. **ObtenirLlistaDeutesREST** Permet consultar la llista de deutes d'un DNI/NIF amb l'ajuntament. Cal introduir:
   - CodiINE10: codi INE10 de l'ajuntament
   - DNINIFContribuent : DNI/NIF del contribuent (8 dígits, sense la lletra de control)
   - Idioma. C: català o E: castellà
1. **ObtenirLlistaDeutesVehicleREST** Permet consultar la llista de deutes d’un vehicle amb l’ajuntament. Cal introduir:
   - CodiINE10: codi INE10 de l'ajuntament
   - DNINIFContribuent : DNI/NIF del contribuent (8 dígits, sense la lletra de control)
   - Idioma. C: català o E: castellà
   - Matrícula: matrícula del vehicle. Exemples de matrícules acceptades: "1234BCD", "1234-BCD", "1234 BCD", "B1234RS", "B-1234-RS", "B 1234 RS"


## Exemples de crides i respostes
A continuació es presenten diversos exemples de crides i respostes. Podeu trobar més informació a:
* **[Especificació swagger]([https://github.com/organisme-de-gestio-tributaria/autoliquidacio-generica/blob/main/swagger%20AutoliquidacioGenerica.json](https://github.com/organisme-de-gestio-tributaria/consulta-deutes-tributaris/blob/main/swagger%20DeutesTributs.json)). Podeu crear el vostre client de forma automàtica a partir d'aquest fitxer.**
* [Comentaris del WSDL](https://wsproves.orgt.diba.cat/deutes/DeutesServiceREST.svc?singleWsdl). Podeu cancel·lar la sol·licitud de certificat a l'accedir al WSDL. Malgrat que aquest wsdl està disponible només per la versió SOAP, els noms dels camps i les explicacions són les mateixes que per la versió REST.
* L’esquema de validació de les dades rebudes es troba en el mateix webservice a: https://wsproves.orgt.diba.cat/deutes/schema/Deutes.xsd 
* Cal notar que totes les dades de tipus text han d'estar en majúscules.

| Endpoint | Mètode HTTP | Exemples |
|---|---|---|
| GenerarDocumentREST | GET | [URL petició](https://wsproves.orgt.diba.cat/Deutes/DeutesServiceREST.svc/GenerarDocumentREST?DNINIFContribuent=00000000&CodiINE10=0810170005&Idioma=C) <br> [Resposta](https://github.com/organisme-de-gestio-tributaria/consulta-deutes-tributaris/blob/main/Exemples/Resposta%20GenerarDocumentREST.json)
| ObtenirLlistaDeutesREST | GET | [URL petició](https://wsproves.orgt.diba.cat/Deutes/DeutesServiceREST.svc/ObtenirLlistaDeutesREST?DNINIFContribuent=00000000&CodiINE10=0810170005&Idioma=C) <br> [Resposta](https://github.com/organisme-de-gestio-tributaria/consulta-deutes-tributaris/blob/main/Exemples/ObtenirLlistaDeutesREST.json)
| ObtenirLlistaDeutesVehicleREST | GET | [URL petició](https://wsproves.orgt.diba.cat/Deutes/DeutesServiceREST.svc/ObtenirLlistaDeutesVehicleREST?DNINIFContribuent=00000000&CodiINE10=0810170005&Idioma=C&Matricula=1234ABC) <br> [Resposta](https://github.com/organisme-de-gestio-tributaria/consulta-deutes-tributaris/blob/main/Exemples/ObtenirLlistaDeutesVehicleREST.json)



