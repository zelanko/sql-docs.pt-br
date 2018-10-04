---
title: Configurar e gerenciar arquivos de dicionário de sinônimos para Pesquisa de Texto Completo | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text indexes [SQL Server], thesaurus files
- thesaurus [full-text search], configuring
- thesaurus [full-text search]
ms.assetid: 3ef96a63-8a52-45be-9a1f-265bff400e54
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3a6d6197cb525ba4ad395da590ea113bdd0a1f0c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48220336"
---
# <a name="configure-and-manage-thesaurus-files-for-full-text-search"></a>Configurar e gerenciar arquivos de dicionário de sinônimos para Pesquisa de texto completo
  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consultas de texto completo podem pesquisar sinônimos de termos especificados pelo usuário com o uso de um dicionário de sinônimos. Um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *dicionário de sinônimos* define um conjunto de sinônimos para um idioma específico. Os administradores de sistema podem definir duas formas de sinônimos: conjuntos de expansão e conjuntos de substituição. Ao desenvolver um dicionário de sinônimos personalizado para seus dados de texto completo, você pode efetivamente ampliar o escopo de consultas de texto completo baseadas nesses dados. Correspondência com o dicionário de sinônimos ocorre para todos os [FREETEXT](/sql/t-sql/queries/freetext-transact-sql) e [FREETEXTABLE](/sql/relational-databases/system-functions/freetexttable-transact-sql) consultas e para quaisquer [CONTAINS](/sql/t-sql/queries/contains-transact-sql) e [CONTAINSTABLE](/sql/relational-databases/system-functions/containstable-transact-sql) consultas que Especifique a cláusula FORMSOF THESAURUS.  
  
##  <a name="tasks"></a> Tarefas básicas para configurar um arquivo de dicionário de sinônimos  
 Para que as consultas de pesquisa de texto completo na sua instância de servidor possam procurar sinônimos em um determinado idioma, defina mapeamentos de dicionário de sinônimos (sinônimos) para esse idioma. Cada dicionário deve ser configurado manualmente para definir o seguinte:  
  
-   Configuração de diacríticos  
  
     Em um determinado dicionário de sinônimos, todos os padrões de pesquisa diferenciam ou não diferenciam marcas diacríticas, como um til (**~**), acento agudo (**´**) ou trema (**¨**), ou seja, eles *diferenciam acentos* ou *não diferenciam acentos*. Por exemplo, vamos supor que você especificou que o padrão "café" deve ser substituído por outros padrões em uma consulta de texto completo. Se o dicionário de sinônimos não diferenciar acentos, a pesquisa de texto completo substituirá os padrões "café" e "cafe". Se o dicionário de sinônimos diferenciar acentos, a pesquisa de texto completo substituirá somente o padrão "café". Por padrão, um dicionário de sinônimos não diferencia acentos.  
  
-   Conjunto de expansão  
  
     Um conjunto de expansão contém um grupo de sinônimos, como "escritor", "autor" e "jornalista", que são substituídos entre si por uma consulta de texto completo. As consultas que contêm uma correspondência para qualquer sinônimo do conjunto de expansão são expandidas para incluir todos os outros sinônimos do conjunto de expansão.  
  
     Para obter mais informações, consulte "Estrutura XML de um conjunto de expansão", mais adiante neste tópico.  
  
-   Conjunto de substituição  
  
     Um conjunto de substituição contém um padrão de texto a ser substituído por um conjunto de substituição. Para ver um exemplo, consulte a seção "Estrutura XML de um conjunto de substituição" posteriormente neste tópico.  
  
  
##  <a name="initial_thesaurus_files"></a> Conteúdo inicial dos arquivos de dicionário de sinônimos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece um conjunto de arquivos XML de dicionário de sinônimos, um para cada idioma com suporte. Esses arquivos estão basicamente vazios. Eles contêm apenas a estrutura XML de alto nível que é comum a todos os dicionários de sinônimos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um dicionário de sinônimos de exemplo comentado.  
  
 Todos os arquivos de dicionário de sinônimos fornecidos com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contêm o seguinte código XML:  
  
```  
<XML ID="Microsoft Search Thesaurus">  
  
<!--  Commented out  
  
    <thesaurus xmlns="x-schema:tsSchema.xml">  
<diacritics_sensitive>0</diacritics_sensitive>  
        <expansion>  
            <sub>Internet Explorer</sub>  
            <sub>IE</sub>  
            <sub>IE5</sub>  
        </expansion>  
        <replacement>  
            <pat>NT5</pat>  
            <pat>W2K</pat>  
            <sub>Windows 2012</sub>  
        </replacement>  
        <expansion>  
            <sub>run</sub>  
            <sub>jog</sub>  
        </expansion>  
    </thesaurus>  
-->  
</XML>  
```  
  
  
##  <a name="location"></a> Local dos arquivos de dicionário de sinônimos  
 A localização padrão dos arquivos de dicionário de sinônimos é esta:  
  
 *< SQL_Server_data_files_path >* \MSSQL12. MSSQLSERVER\MSSQL\FTDATA\  
  
 Esse local padrão contém os seguintes arquivos:  
  
-   Arquivos de dicionário de sinônimos específicos de um idioma  
  
     Durante a instalação, arquivos vazios do dicionário de sinônimos são instalados no local indicado acima. Um arquivo à parte é fornecido para cada idioma suportado. Um administrador de sistema pode personalizar esses arquivos.  
  
     Os nomes de arquivo padrão dos arquivos de dicionário de sinônimos usam o seguinte formato:  
  
     'ts' + \<abreviação do idioma de três letras > + '. XML'  
  
     O nome do arquivo de dicionário de sinônimos de um idioma é especificado no Registro no seguinte valor: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\\<nome-da-instância>\MSSearch\\<abreviação-do-idioma>.  
  
-   O arquivo de dicionário de sinônimos global  
  
     Um arquivo de dicionário de sinônimos global vazio, tsGlobal.xml.  
  
 Você pode alterar a localização e os nomes de um arquivo de dicionário de sinônimos mudando a respectiva chave do Registro. Para cada idioma, a localização do arquivo de dicionário de sinônimos é especificada no seguinte valor do Registro:  
  
 HKLM/SOFTWARE/Microsoft/Microsoft SQL Server /\<nome da instância>/MSSearch/Language/\<abreviação do idioma > / TsaurusFile  
  
 O arquivo de dicionário de sinônimos global corresponde ao idioma Neutro com LCID 0. Esse valor só pode ser alterado por administradores.  
  
  
##  <a name="how_queries_use_tf"></a> Como os arquivos de dicionário de sinônimos de uso de consultas  
 Uma consulta ao dicionário de sinônimos usa um dicionário de sinônimos específico de um idioma e o dicionário de sinônimos global. Primeiro, a consulta pesquisa pelo arquivo específico do idioma e depois o carrega para ser processado (a menos que já esteja carregado). A consulta é expandida para incluir os sinônimos específicos do idioma definidos pelos conjuntos de expansão e regras de substituição no arquivo do dicionário de sinônimos. Essas etapas são repetidas para o dicionário de sinônimos global. Entretanto, se um termo já tiver correspondências no arquivo de dicionário de sinônimos específico do idioma, ele não terá correspondentes no dicionário de sinônimos global.  
  
  
##  <a name="structure"></a> Entendendo a estrutura de um arquivo de dicionário de sinônimos  
 Cada arquivo de dicionário de sinônimos define um contêiner XML cuja ID é `Microsoft Search Thesaurus`, além de um comentário, `<!--` … `-->`, que contém um dicionário de sinônimos de exemplo. O dicionário de sinônimos é definido em um \<dicionário de sinônimos > elemento que contém exemplos dos elementos filho que definem a configuração de diacríticos, os conjuntos de expansão e conjuntos de substituição, da seguinte maneira:  
  
-   Estrutura XML da configuração de diacríticos  
  
     A configuração de diacríticos de um dicionário de sinônimos é especificada em um único elemento <diacritics_sensitive>. Esse elemento contém um valor de inteiro que controla a distinção de acentos, da seguinte maneira:  
  
    |Configuração de diacríticos|Valor|XML|  
    |------------------------|-----------|---------|  
    |não diferenciam acentos|0|`<diacritics_sensitive>0</diacritics_sensitive>`|  
    |diferenciam acentos|1|`<diacritics_sensitive>1</diacritics_sensitive>`|  
  
    > [!NOTE]  
    >  Essa configuração só pode ser aplicada uma vez no arquivo e é válida para todos os padrões de pesquisa do arquivo. Essa configuração não pode ser especificada para padrões individuais.  
  
-   Estrutura XML de um conjunto de expansão  
  
     Cada conjunto de expansão é incluído em um \<expansão > elemento. Esse elemento, você especifica um ou mais substituições em um \<sub > elemento. No conjunto de expansão, você pode especificar um grupo de substituições sinônimas umas das outras.  
  
     Por exemplo, você pode editar a seção de expansão para tratar as substituições "escritor", "autor" e "jornalista" como sinônimos. As consultas de pesquisa de texto completo que contêm correspondências em uma substituição são expandidas para incluir todas as outras substituições especificadas no conjunto de expansão. Por isso, no exemplo anterior, quando você emite uma consulta FORMS OF THESAURUS ou FREETEXT para a palavra "autor", a pesquisa de texto completo também retorna resultados que contêm as palavras "escritor" e "jornalista".  
  
     A seção de conjuntos de expansão do exemplo anterior seria parecida com esta:  
  
    ```  
    <expansion>  
            <sub>writer</sub>  
            <sub>author</sub>  
            <sub>journalist</sub>  
    </expansion>  
    ```  
  
-   Estrutura XML de um conjunto de substituição  
  
     Cada conjunto de substituição é incluído em um \<substituição > elemento. Dentro desse elemento, você pode especificar um ou mais padrões em uma \<pat > elemento e zero ou mais substituições em \<sub > elementos, um por sinônimo. Também pode especificar um padrão a ser substituído por um conjunto de substituição. Padrões e substituições podem conter uma palavra ou uma sequência de palavras. Se não houver uma substituição especificada para um padrão, isso será o mesmo que remover o padrão da consulta do usuário.  
  
     Por exemplo, vamos supor que você deseja que as consultas relacionadas ao termo "Win8", o padrão, sejam substituídas por "Windows Server 2012" ou "Windows 8.0", as substituições. Se você executar uma consulta de texto completo usando o termo "Win8", a pesquisa de texto completo retornará apenas resultados que contenham "Windows Server 2012" ou "Windows 8.0", e não resultados que contenham "Win8". Isso acontece porque o padrão "Win8" foi “substituído” pelos padrões "Windows Server 2012" e "Windows 8.0".  
  
     A seção de conjuntos de substituição procuraria o seguinte para o exemplo anterior:  
  
    ```  
    <replacement>  
            <pat>Win8</pat>  
            <sub>Windows Server 2012</sub>  
            <sub>Windows 8.0</sub>  
    </replacement>  
    ```  
  
     Se você tiver dois conjuntos de substituição com padrões semelhantes sendo associados, o mais longo dos dois tem precedência. Por exemplo, ao executar a consulta FORMS OF THESAURUS para "comunidade online do Internet Explorer" com os conjuntos de substituição a seguir, o conjunto de substituição "Internet Explorer" tem precedência sobre o conjunto de substituição "Internet". Portanto, essa consulta será processada como "comunidade online do IE" ou "comunidade online do IE 9".  
  
    ```  
    <replacement>  
             <pat>Internet</pat>  
             <sub>intranet</sub>  
    </replacement>  
    ```  
  
     e  
  
    ```  
    <replacement>  
             <pat>Internet Explorer</pat>  
             <sub>IE</sub>  
             <sub>IE 9</sub>  
    </replacement>  
    ```  
  
  
##  <a name="working_with_thesaurus_files"></a> Trabalhando com arquivos de dicionário de sinônimos  
 **Para editar um arquivo de dicionário de sinônimos**  
  
-   [Editar um arquivo de dicionário de sinônimos](#editing)  
  
 **Para carregar um arquivo de dicionário de sinônimos atualizado**  
  
-   [sp_fulltext_load_thesaurus_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql)  
  
 **Para exibir o resultado da geração de tokens de uma combinação de separador, dicionário de sinônimos e lista de palavras irrelevantes do word**  
  
-   [sys.dm_fts_parser &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql)  
  
  
##  <a name="editing"></a> Editar um arquivo de dicionário de sinônimos  
 É possível configurar o dicionário de sinônimos de um idioma editando seu arquivo (um arquivo XML). Durante a instalação, arquivos vazios do dicionário de sinônimos que contêm apenas os \<xml > contêiner e um exemplo comentado \<dicionário de sinônimos > elemento estão instalados. As consultas de pesquisa de texto completo que procuram sinônimos funcionem adequadamente, você deve criar um real \<dicionário de sinônimos > elemento que define um conjunto de sinônimos. Você pode definir duas formas de sinônimos: conjuntos de expansão e conjuntos de substituição.  
  
 **Restrições para arquivos de dicionário de sinônimos**  
  
 As seguintes restrições se aplicam à edição de um arquivo de dicionário de sinônimos:  
  
-   Somente administradores do sistema podem atualizar, modificar ou excluir arquivos de dicionário de sinônimos.  
  
-   Ao editar arquivos de dicionários de sinônimos usando ferramentas de editores de texto, é necessário salvá-los no formato Unicode e especificar Marcas de Ordem de Byte.  
  
-   As entradas de dicionário de sinônimos não podem estar vazias, nem pode haver separação de palavras para uma cadeia de caracteres vazia.  
  
-   As frases no arquivo de dicionário de sinônimos não devem ter mais de 512 caracteres.  
  
-   Um dicionário de sinônimos não deve conter entradas duplicadas entre as \<sub > entradas de conjuntos de expansão e o \<pat > elementos de conjuntos de substituição.  
  
 **Recomendações para arquivos de dicionário de sinônimos**  
  
 Recomendamos que as entradas no arquivo do dicionário de sinônimos não contenham caracteres especiais. Isso ocorre porque os separadores de palavras têm comportamentos sutis em relação a caracteres especiais. Se uma entrada de dicionário de sinônimos contiver caracteres especiais, os separadores de palavras usados com essa entrada poderão ter implicações de comportamento sutis para uma consulta de texto completo.  
  
 É recomendável que \<sub > entradas de não contenham palavras irrelevantes pois tais palavras são omitidas do índice de texto completo. As consultas são expandidas para incluir a \<sub > entradas de um arquivo de dicionário de sinônimos e se um \<sub > contiver palavras irrelevantes, o tamanho da consulta aumentará desnecessariamente.  
  
#### <a name="to-edit-a-thesaurus-file"></a>Para editar um arquivo de dicionário de sinônimos  
  
1.  Abra o arquivo de dicionário de sinônimos no Bloco de Notas.  
  
2.  Se você estiver editando um arquivo de dicionário de sinônimos pela primeira vez, remova as seguintes linhas de comentário no início e final do arquivo, respectivamente:  
  
    ```  
    <!--Commented out  
    -->  
    ```  
  
3.  Adicione, modifique ou exclua um conjunto de substituições ou conjunto de expansão.  
  
4.  Salve o arquivo e feche o Bloco de Notas.  
  
5.  Use [sp_fulltext_load_thesaurus_file](/sql/relational-databases/system-stored-procedures/sp-fulltext-load-thesaurus-file-transact-sql) para carregar o conteúdo do arquivo de dicionário de sinônimos no tempdb, especificando o LCID (identificador de localidade) correspondente ao idioma do arquivo. Por exemplo, para o arquivo de dicionário de sinônimos em inglês, tsenu.xml, o LCID correspondente é 1033.  
  
    ```  
    USE AdventureWorks2012 ;  
    EXEC sys.sp_fulltext_load_thesaurus_file 1033;  
    GO  
    ```  
  
  
## <a name="see-also"></a>Consulte também  
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/containstable-transact-sql)   
 [FREETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/freetext-transact-sql)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/freetexttable-transact-sql)   
 [Pesquisa de Texto Completo](full-text-search.md)  
  
  
