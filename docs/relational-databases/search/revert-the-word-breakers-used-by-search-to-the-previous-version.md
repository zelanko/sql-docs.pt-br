---
title: "Reverter os separadores de palavras usados por pesquisa à versão anterior | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 29b4488e-4c6a-4bf0-a64d-19e2fdafa7ae
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2549481c3e09e4b052e0eea40c993ccf191f38ba
ms.contentlocale: pt-br
ms.lasthandoff: 07/31/2017

---
# <a name="revert-the-word-breakers-used-by-search-to-the-previous-version"></a>Reverter os separadores de palavras usados por pesquisa à versão anterior
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instala e habilita uma versão dos separadores de palavras e lematizadores para todos os idiomas com suporte de Pesquisa de Texto Completo com a exceção de coreano. Este tópico descreve como alternar deste nova versão desses componentes para a versão anterior, ou alternar da versão anterior para a nova versão.  
  
 Este tópico não discute os seguintes idiomas:  
  
-   **Inglês**. A fim de reverter ou restaurar os componentes em inglês, consulte [Change the Word Breaker Used for US English and UK English](../../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md).  
  
-   **Dinamarquês, polonês e turco**. Separadores de palavras de terceiros para dinamarquês, polonês e turco que foram incluídos com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foram substituídos por componentes do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
-   **Tcheco e grego**. Há novos separadores de palavras para tcheco e grego. As versões anteriores de Pesquisa de Texto Completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não incluíam suporte para estes dois idiomas.  
  
-   **Coreano**. O separador de palavras e o lematizador para o idioma coreano não são atualizados nesta versão.  
  
 Para obter informações gerais sobre separadores de palavras e lematizadores, consulte [Configurar e gerenciar separadores de palavras e lematizadores de pesquisa](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
##  <a name="overview"></a> Visão geral de como reverter e restaurar separadores de palavras e lematizadores  
 As instruções para reverter e restaurar separadores de palavras e lematizadores dependem do idioma. A tabela a seguir resume os 3 conjuntos de ações que podem ser exigidas para reverter para a versão anterior dos componentes.  
  
|Arquivo atual|Arquivo anterior|Número de idiomas afetados|Ação para arquivos|Ação para entradas do Registro|  
|------------------|-------------------|----------------------------------|----------------------|---------------------------------|  
|NaturalLanguage6.dll|NaturalLanguage6.dll|34|Obter e instalar uma versão anterior de NaturalLanguage6.dll, substituindo a versão atual do arquivo.|Não é necessário fazer nada.<br /><br /> As chaves do Registro e os valores não foram alterados para esta versão.|  
|(Outro nome do arquivo)|NaturalLanguage6.dll|5|Obter e instalar uma versão anterior de NaturalLanguage6.dll, substituindo a versão atual do arquivo.|Alterar um conjunto de entradas do Registro para especificar a versão anterior dos componentes.|  
|(Outro nome do arquivo)|(Outro nome do arquivo)|6|Não é necessário fazer nada.<br /><br /> [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] copia a versão atual e a anterior dos componentes para a pasta Binn.|Alterar um conjunto de entradas do Registro para especificar a versão anterior dos componentes.|  
  
> [!WARNING]  
>  Se você substituir a versão atual do arquivo NaturalLanguage6.dll por uma versão diferente, o comportamento de todos os idiomas que usam este arquivo será afetado.  
  
 Os arquivos descritos neste tópico são arquivos DLL instalados na pasta `MSSQL\Binn` para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O caminho completo é geralmente o seguinte:  
  
 `C:\Program Files\Microsoft SQL Server\<instance>\MSSQL\Binn`  
  
##  <a name="nl6nl6"></a> Idiomas para os quais o nome de arquivo do separador de palavras atual e do anterior é NaturalLanguage6.dll  
 Para os idiomas na tabela a seguir, o nome de arquivo do separador de palavras atual e do anterior é NaturalLanguage6.dll. A fim de reverter ou restaurar estes componentes, você tem que substituir NaturalLanguage6.dll por uma versão diferente do mesmo arquivo. Você não tem que alterar as entradas do Registro, porque elas não foram alteradas para esta versão.  
  
> [!WARNING]  
>  Se você substituir a versão atual do arquivo NaturalLanguage6.dll por uma versão diferente, o comportamento de todos os idiomas que usam este arquivo será afetado.  
  
 **Lista de idiomas afetados**  
  
|Idioma|Abreviação<br />usado no<br />Registro|LCID|  
|--------------|---------------------------------------|----------|  
|Bengali|ben|1093|  
|Búlgaro|bgr|1026|  
|Catalão|cat|1027|  
|Espanhol|esn|3082|  
|Francês|fra|1036|  
|Guzerati|guj|1095|  
|Hebraico|heb|1037|  
|Híndi|hin|1081|  
|Croata|hrv|1050|  
|Indonésio|ind|1057|  
|Islandês|isl|1039|  
|Italiano|ita|1040|  
|Kannada|kan|1099|  
|Lituano|lth|1063|  
|Letão|lvi|1062|  
|Malaiala|mal|1100|  
|Marati|mar|1102|  
|Malaio|msl|1086|  
|Neutro|Neutro|0000|  
|Norueguês (Bokmål)|e|1044|  
|Punjabi|pan|1094|  
|Português (Brasil)|ptb|1046|  
|Português|ptg|2070|  
|Romeno|rom|1048|  
|Eslovaco|sky|1051|  
|Esloveno|slv|1060|  
|Sérvio - Cirílico|srb|3098|  
|Sérvio - latino|srl|2074|  
|Sueco|sve|1053|  
|Tâmil|tam|1097|  
|Télugo|tel|1098|  
|Ucraniano|ukr|1058|  
|Urdu|urd|1056|  
|Vietnamita|vit|1066|  
  
 A tabela acima está classificada alfabeticamente na coluna de Abreviação.  
  
###  <a name="nl6nl6revert"></a> Para reverter para os componentes anteriores  
  
1.  Navegue até a pasta Binn descrita acima.  
  
2.  Faça backup da versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do arquivo NaturalLanguage6.dll para outro local.  
  
3.  Copie a versão anterior de NaturalLanguage6.dll da pasta Binn de uma instância do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] para a pasta Binn da instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
    > [!WARNING]  
    >  Esta alteração afeta todos os idiomas que usam NaturalLanguage6.dll na versão anterior atual e na anterior.  
  
4.  Reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
###  <a name="nl6nl6restore"></a> Para restaurar os componentes atuais  
  
1.  Navegue até o local onde você fez backup da versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do arquivo NaturalLanguage6.dll.  
  
2.  Copie a versão atual de NaturalLanguage6.dll do local de backup para a pasta Binn da instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
    > [!WARNING]  
    >  Esta alteração afeta todos os idiomas que usam NaturalLanguage6.dll na versão anterior atual e na anterior.  
  
3.  Reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
##  <a name="newnl6"></a> Idiomas para os quais o nome de arquivo somente do separador de palavras anterior é NaturalLanguage6.dll  
 Para os idiomas na tabela a seguir, o nome de arquivo do separador de palavras anterior é diferente do nome de arquivo da nova versão. O nome do arquivo anterior é NaturalLanguage6.dll. A fim de reverter para a versão anterior, você tem que substituir a versão atual do NaturalLanguage6.dll por uma versão anterior do mesmo arquivo. Você também tem que alterar um conjunto de entradas do Registro para especificar a versão anterior ou a atual dos componentes.  
  
> [!WARNING]  
>  Se você substituir a versão atual do arquivo NaturalLanguage6.dll por uma versão diferente, o comportamento de todos os idiomas que usam este arquivo será afetado.  
  
 **Lista de idiomas afetados**  
  
|Idioma|Abreviação<br />usado no<br />Registro|LCID|  
|--------------|---------------------------------------|----------|  
|Árabe|ara|1025|  
|Alemão|deu|1031|  
|Japonês|jpn|1041|  
|Holandês|nld|1043|  
|Russo|rus|1049|  
  
 A tabela acima está classificada alfabeticamente na coluna de Abreviação.  
  
 Use as instruções a seguir junto com a lista de valores na seção [Nomes de arquivo e valores do Registro para reverter e restaurar separadores de palavras e lematizadores](#newnl6values).  
  
###  <a name="newnl6revert"></a> Para reverter para os componentes anteriores  
  
1.  Navegue até a pasta Binn descrita acima.  
  
2.  Não remova os arquivos para a versão atual dos componentes da pasta Binn.  
  
3.  Faça backup da versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do arquivo NaturalLanguage6.dll para outro local.  
  
4.  Copie a versão anterior de NaturalLanguage6.dll da pasta Binn de uma instância do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] para a pasta Binn da instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
    > [!WARNING]  
    >  Esta alteração afeta todos os idiomas que usam NaturalLanguage6.dll na versão anterior atual e na anterior.  
  
5.  No Registro, navegue até o nó: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<InstanceRoot>\MSSearch\CLSID**.  
  
6.  Use as etapas a seguir para adicionar novas chaves para as ClassIDs COM para o separador de palavras e as interfaces de lematizador anteriores para os idiomas selecionados:  
  
    1.  Adicione uma nova chave com o valor da tabela para o separador de palavras anterior.  
  
    2.  Atualize os dados (Padrão) dessa chave de valor para o nome de arquivo do separador de palavras anterior da tabela.  
  
    3.  Se o idioma selecionado usar um lematizador, adicione uma nova chave com o valor da tabela para o lematizador anterior.  
  
    4.  Se o idioma selecionado usar um lematizador, atualize os dados (Padrão) desse valor de chave para o nome de arquivo do lematizador anterior da tabela.  
  
7.  No Registro, navegue até o seguinte nó: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<InstanceRoot>\MSSearch\Language\<language_key>**. *<language_key>* representa a abreviação para o idioma que é usado no Registro; por exemplo, "fra" para o francês e "esn" para espanhol.  
  
8.  Atualize o valor de chave **WBreakerClass** para o valor da tabela para o separador de palavras atual.  
  
9. Se o idioma selecionado usar um lematizador, atualize o valor de chave **StemmerClass** para o valor da tabela para o lematizador atual.  
  
10. Reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
###  <a name="newnl6restore"></a> Para restaurar os componentes atuais  
  
1.  Navegue até o local onde você fez backup da versão do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] do arquivo NaturalLanguage6.dll.  
  
2.  Copie a versão atual de NaturalLanguage6.dll do local de backup para a pasta Binn da instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
    > [!WARNING]  
    >  Esta alteração afeta todos os idiomas que usam NaturalLanguage6.dll na versão anterior atual e na anterior.  
  
3.  No Registro, navegue até o nó: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<InstanceRoot>\MSSearch\CLSID**.  
  
4.  Se as chaves a seguir não existirem, use as etapas a seguir para adicionar novas chaves para as ClassIDs COM para o separador de palavras atual e interfaces de lematizador para o idioma selecionado:  
  
    1.  Adicione uma nova chave com o valor da tabela para o separador de palavras atual.  
  
    2.  Atualize os dados (Padrão) dessa chave de valor para o nome de arquivo do separador de palavras atual da tabela.  
  
    3.  Se o idioma selecionado usar um lematizador, adicione uma nova chave com o valor da tabela para o lematizador atual.  
  
    4.  Se o idioma selecionado usar um lematizador, atualize os dados (Padrão) desse valor de chave para o nome de arquivo do lematizador atual da tabela.  
  
5.  No Registro, navegue até o seguinte nó: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<InstanceRoot>\MSSearch\Language\<language_key>**. *<language_key>* representa a abreviação para o idioma que é usado no Registro; por exemplo, "fra" para o francês e "esn" para espanhol.  
  
6.  Atualize o valor de chave **WBreakerClass** para o valor da tabela para o separador de palavras anterior.  
  
7.  Se o idioma selecionado usar um lematizador, atualize o valor de chave **StemmerClass** para o valor da tabela para o lematizador anterior.  
  
8.  Reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
###  <a name="newnl6values"></a> Nomes de arquivo e valores do Registro para reverter e restaurar separadores de palavras e lematizadores  
 Use a lista de nomes de arquivos e entradas do Registro a seguir junto com as instruções na seção acima. Use os valores anteriores para reverter à versão anterior ou use os valores atuais para restaurar a versão atual dos componentes.  
  
 A lista a seguir está classificada alfabeticamente na abreviação usada para cada idioma.  
  
 **Árabe (ara), LCID 1025**  
  
|Componente|Separador de palavras|Lematizador|  
|---------------|------------------|-------------|  
|CLSID anterior|7EFD3C7E-9E4B-4a93-9503-DECD74C0AC6D|483B0283-25DB-4c92-9C15-A65925CB95CE|  
|Nome de arquivo anterior|NaturalLanguage6.dll|NaturalLanguage6.dll|  
|CLSID atual|04b37e30-c9a9-4a7d-8f20-792fc87ddf71|Nenhuma|  
|Nome do arquivo atual|MSWB7.dll|Nenhuma|  
  
 **Alemão (deu), LCID 1031**  
  
|Componente|Separador de palavras|Lematizador|  
|---------------|------------------|-------------|  
|CLSID anterior|45EACA36-DBE9-4e4a-A26D-5C201902346D|65170AE4-0AD2-4fa5-B3BA-7CD73E2DA825|  
|Nome de arquivo anterior|NaturalLanguage6.dll|NaturalLanguage6.dll|  
|CLSID atual|dfa00c33-bf19-482e-a791-3c785b0149b4|8a474d89-6e2f-419c-8dd5-9b50edc8c787|  
|Nome do arquivo atual|MSWB7.dll|MSWB7.dll|  
  
 **Japonês (jpn), LCID 1041**  
  
|Componente|Separador de palavras|Lematizador|  
|---------------|------------------|-------------|  
|CLSID anterior|E1E8F15E-8BEC-45df-83BF-50FF84D0CAB5|3D5DF14F-649F-4cbc-853D-F18FEDE9CF5D|  
|Nome de arquivo anterior|NaturalLanguage6.dll|NaturalLanguage6.dll|  
|CLSID atual|04096682-6ece-4e9e-90c1-52d81f0422ed|Nenhuma|  
|Nome do arquivo atual|MsWb70011.dll|Nenhuma|  
  
 **Holandês (nld), LCID 1043**  
  
|Componente|Separador de palavras|Lematizador|  
|---------------|------------------|-------------|  
|CLSID anterior|2C9F6BEB-C5B0-42b6-A5EE-84C24DC0D8EF|F7A465EE-13FB-409a-B878-195B420433AF|  
|Nome de arquivo anterior|NaturalLanguage6.dll|NaturalLanguage6.dll|  
|CLSID atual|69483c30-a9af-4552-8f84-a0796ad5285b|CF923CB5-1187-43ab-B053-3E44BED65FFA|  
|Nome do arquivo atual|MSWB7.dll|MSWB7.dll|  
  
 **Russo (rus), LCID 1049**  
  
|Componente|Separador de palavras|Lematizador|  
|---------------|------------------|-------------|  
|CLSID anterior|2CB6CDA4-1C14-4392-A8EC-81EEF1F2E079|E06A0DDD-E81A-4e93-8A8D-F386C3A1B670|  
|Nome de arquivo anterior|NaturalLanguage6.dll|NaturalLanguage6.dll|  
|CLSID atual|aaa3d3bd-6de7-4317-91a0-d25e7d3babc3|d42c8b70-adeb-4b81-a52f-c09f24f77dfa|  
|Nome do arquivo atual|MSWB7.dll|MSWB7.dll|  
  
##  <a name="newnew"></a> Idiomas para os quais nem o nome de arquivo atual ou anterior é NaturalLanguage6.dll  
 Para os idiomas na tabela a seguir, os nomes de arquivo dos separadores de palavras e lematizadores anteriores são diferentes dos nomes de arquivo das novas versões. Nem o nome de arquivo atual nem o anterior é NaturalLanguage6.dll. Você não tem que substituir os arquivos, porque a instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] copia a versão atual e a anterior dos componentes para a pasta Binn. No entanto, você também tem que alterar um conjunto de entradas do Registro para especificar a versão anterior ou a atual dos componentes.  
  
 **Lista de idiomas afetados**  
  
|Idioma|Abreviação<br />usado no<br />Registro|LCID|  
|--------------|---------------------------------------|----------|  
|Chinês simplificado|chs|2052|  
|Chinês tradicional|cht|1028|  
|Tailandês|tha|1054|  
|Chinês tradicional|zh-hk|3076|  
|Chinês tradicional|zh-mo|5124|  
|Chinês simplificado|zh-sg|4100|  
  
 A tabela acima está classificada alfabeticamente na coluna de Abreviação.  
  
 Use as instruções a seguir junto com a lista de valores na seção [Nomes de arquivo e valores do Registro para reverter e restaurar separadores de palavras e lematizadores](#newnewvalues).  
  
###  <a name="newnewrevert"></a> Para reverter para os componentes anteriores  
  
1.  Não remova os arquivos para a versão atual dos componentes da pasta Binn.  
  
2.  No Registro, navegue até o nó: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<InstanceRoot>\MSSearch\CLSID**.  
  
3.  Use as etapas a seguir para adicionar novas chaves para as ClassIDs COM para o separador de palavras e as interfaces de lematizador anteriores para os idiomas selecionados:  
  
    1.  Adicione uma nova chave com o valor da tabela para o separador de palavras anterior.  
  
    2.  Atualize os dados (Padrão) dessa chave de valor para o nome de arquivo do separador de palavras anterior da tabela.  
  
    3.  Se o idioma selecionado usar um lematizador, adicione uma nova chave com o valor da tabela para o lematizador anterior.  
  
    4.  Se o idioma selecionado usar um lematizador, atualize os dados (Padrão) desse valor de chave para o nome de arquivo do lematizador anterior da tabela.  
  
4.  No Registro, navegue até o seguinte nó: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<InstanceRoot>\MSSearch\Language\<language_key>**. *<language_key>* representa a abreviação para o idioma que é usado no Registro; por exemplo, "fra" para o francês e "esn" para espanhol.  
  
5.  Atualize o valor de chave **WBreakerClass** para o valor da tabela para o separador de palavras atual.  
  
6.  Se o idioma selecionado usar um lematizador, atualize o valor de chave **StemmerClass** para o valor da tabela para o lematizador atual.  
  
7.  Reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
###  <a name="newnewrestore"></a> Para restaurar os componentes anteriores  
  
1.  Não remova os arquivos para a versão anterior dos componentes da pasta Binn.  
  
2.  No Registro, navegue até o nó: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<InstanceRoot>\MSSearch\CLSID**.  
  
3.  Se as chaves a seguir não existirem, use as etapas a seguir para adicionar novas chaves para as ClassIDs COM para o separador de palavras atual e interfaces de lematizador para o idioma selecionado:  
  
    1.  Adicione uma nova chave com o valor da tabela para o separador de palavras atual.  
  
    2.  Atualize os dados (Padrão) dessa chave de valor para o nome de arquivo do separador de palavras atual da tabela.  
  
    3.  Se o idioma selecionado usar um lematizador, adicione uma nova chave com o valor da tabela para o lematizador atual.  
  
    4.  Se o idioma selecionado usar um lematizador, atualize os dados (Padrão) desse valor de chave para o nome de arquivo do lematizador atual da tabela.  
  
4.  No Registro, navegue até o seguinte nó: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\<InstanceRoot>\MSSearch\Language\<language_key>**. *<language_key>* representa a abreviação para o idioma que é usado no Registro; por exemplo, "fra" para o francês e "esn" para espanhol.  
  
5.  Atualize o valor de chave **WBreakerClass** para o valor da tabela para o separador de palavras anterior.  
  
6.  Se o idioma selecionado usar um lematizador, atualize o valor de chave **StemmerClass** para o valor da tabela para o lematizador anterior.  
  
7.  Reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
###  <a name="newnewvalues"></a> Nomes de arquivo e valores do Registro para reverter e restaurar separadores de palavras e lematizadores  
 Use a lista de nomes de arquivos e entradas do Registro a seguir junto com as instruções na seção acima. Use os valores anteriores para reverter à versão anterior ou use os valores atuais para restaurar a versão atual dos componentes.  
  
 A lista a seguir está classificada alfabeticamente na abreviação usada para cada idioma.  
  
 **Chinês simplificado (chs), LCID 2052**  
  
|Componente|Separador de palavras|  
|---------------|------------------|  
|CLSID anterior|12CE94A0-DEFB-11D2-B31D-00600893A857|  
|Nome de arquivo anterior|chsbrkr.dll|  
|CLSID atual|E0831C90-BAB0-4ca5-B9BD-EA254B538DAC|  
|Nome do arquivo atual|MsWb70804.dll|  
  
 **Chinês tradicional (cht), LCID 1028**  
  
|Componente|Separador de palavras|  
|---------------|------------------|  
|CLSID anterior|1680E7C3-9430-4A51-9B82-1E7E7AEE5258|  
|Nome de arquivo anterior|chtbrkr.dll|  
|CLSID atual|E9B1DF65-08F1-438b-8277-EF462B23A792|  
|Nome do arquivo atual|MsWb70404.dll|  
  
 **Tailandês (tha), LCID 1054**  
  
|Componente|Separador de palavras|Lematizador|  
|---------------|------------------|-------------|  
|CLSID anterior|CCA22CF4-59FE-11D1-BBFF-00C04FB97FDA|CEDC01C7-59FE-11D1-BBFF-00C04FB97FDA|  
|Nome de arquivo anterior|Thawbrkr.dll|Thawbrkr.dll|  
|CLSID atual|F70C0935-6E9F-4ef1-9F06-7876536DB900|Nenhuma|  
|Nome do arquivo atual|MsWb7001e.dll|Nenhuma|  
  
 **Chinês tradicional (zh-hk), LCID 3076**  
  
|Componente|Separador de palavras|  
|---------------|------------------|  
|CLSID anterior|1680E7C3-9430-4A51-9B82-1E7E7AEE5258|  
|Nome de arquivo anterior|chtbrkr.dll|  
|CLSID atual|E9B1DF65-08F1-438b-8277-EF462B23A792|  
|Nome do arquivo atual|MsWb70404.dll|  
  
 **Chinês tradicional (zh-mo), LCID 5124**  
  
|Componente|Separador de palavras|  
|---------------|------------------|  
|CLSID anterior|1680E7C3-9430-4A51-9B82-1E7E7AEE5258|  
|Nome de arquivo anterior|chtbrkr.dll|  
|CLSID atual|E9B1DF65-08F1-438b-8277-EF462B23A792|  
|Nome do arquivo atual|MsWb70404.dll|  
  
 **Chinês simplificado (zh-sg), LCID 4100**  
  
|Componente|Separador de palavras|  
|---------------|------------------|  
|CLSID anterior|12CE94A0-DEFB-11D2-B31D-00600893A857|  
|Nome de arquivo anterior|chsbrkr.dll|  
|CLSID atual|E0831C90-BAB0-4ca5-B9BD-EA254B538DAC|  
|Nome do arquivo atual|MsWb70804.dll|  
  
## <a name="see-also"></a>Consulte também  
 [Change the Word Breaker Used for US English and UK English](../../relational-databases/search/change-the-word-breaker-used-for-us-english-and-uk-english.md)   
 [Alterações de comportamento em pesquisa de texto completo](http://msdn.microsoft.com/library/573444e8-51bc-4f3d-9813-0037d2e13b8f)  
  
  
