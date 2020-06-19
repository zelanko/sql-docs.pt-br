---
title: Manter valores nulos ou usar os valores padrão durante a importação em massa (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], null values
- bulk importing [SQL Server], default values
- data formats [SQL Server], null values
- bulk rowset providers [SQL Server]
- bcp utility [SQL Server], null values
- BULK INSERT statement
- default values
- OPENROWSET function, bulk importing
- data formats [SQL Server], default values
ms.assetid: 6b91d762-337b-4345-a159-88abb3e64a81
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 856aa12f6ad5e5094324e0df65941bc63d611451
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85026692"
---
# <a name="keep-nulls-or-use-default-values-during-bulk-import-sql-server"></a>Manter valores nulos ou use os valores padrão durante a importação em massa (SQL Server)
  Por padrão, quando os dados são importados para uma tabela, o comando **bcp** e a instrução BULK INSERT observam os padrões definidos para as colunas na tabela. Por exemplo, se houver um campo nulo em um arquivo de dados, o valor padrão para a coluna será carregado no campo nulo. O comando **bcp** e a instrução BULK INSERT permitem que você especifique a retenção de campos nulos.  
  
 Em contraste, uma instrução INSERT regular retém o valor nulo em vez de inserir um valor padrão. A instrução INSERT ... SELECT * FROM OPENROWSET(BULK...) fornece o mesmo comportamento básico de INSERT regular, mas, além disso, dá suporte a uma dica de tabela para inserir os valores padrão.  
  
> [!NOTE]  
>  Para arquivos de formato de exemplo que ignoram uma coluna de tabela, veja [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md).  
  
## <a name="sample-table-and-data-file"></a>Tabela e arquivo de dados de exemplo  
 Para executar os exemplos neste tópico, é necessário criar uma tabela e um arquivo de dados de exemplo.  
  
### <a name="sample-table"></a>Tabela de exemplo  
 Os exemplos requerem que uma tabela denominada **MyTestDefaultCol2** seja criada no banco de dados de exemplo **AdventureWorks** no esquema **dbo** . Para criar esta tabela, no Editor de Consultas do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , execute:  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE MyTestDefaultCol2   
(Col1 smallint,  
Col2 nvarchar(50) DEFAULT 'Default value of Col2',  
Col3 nvarchar(50)   
);  
GO  
  
```  
  
 Observe que a segunda coluna de tabela, `Col2`, tem um valor padrão.  
  
### <a name="sample-format-file"></a>Arquivo de formato de exemplo  
 Alguns dos exemplos de importação em massa usam um formato de arquivo não XML, `MyTestDefaultCol2-f-c.Fmt` que correspondem exatamente à tabela `MyTestDefaultCol2`. Para criar esse arquivo de formato, no prompt de comando do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, digite:  
  
```  
bcp AdventureWorks..MyTestDefaultCol2 format nul -c -f C:\MyTestDefaultCol2-f-c.Fmt -t, -r\n -T  
  
```  
  
 Para obter mais informações sobre como criar arquivos de formato, veja [Criar um arquivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md).  
  
### <a name="sample-data-file"></a>Arquivo de dados de exemplo  
 O exemplo usa um arquivo de dados de exemplo, `MyTestEmptyField2-c.Dat`, que não contém nenhum valor no segundo campo. O arquivo de dados `MyTestEmptyField2-c.Dat` contém os registros a seguir.  
  
```  
1,,DataField3  
2,,DataField3  
  
```  
  
## <a name="keeping-null-values-with-bcp-or-bulk-insert"></a>Mantendo valores nulos com bcp ou BULK INSERT  
 Os qualificadores a seguir especificam que um campo vazio no arquivo de dados retém seu valor nulo durante a operação de importação em massa, em vez de herdar um valor padrão (se houver) para as colunas de tabela.  
  
|Comando|Qualificador|Tipo de qualificador|  
|-------------|---------------|--------------------|  
|**bcp**|`-k`|Opção|  
|BULK INSERT|KEEPNULLS<sup>1</sup>|Argumento|  
  
 <sup>1</sup> para BULK INSERT, se os valores padrão não estiverem disponíveis, a coluna da tabela deverá ser definida para permitir valores nulos.  
  
> [!NOTE]  
>  Esses qualificadores desabilitam a verificação de definições DEFAULT em uma tabela por esses comandos de importação em massa. No entanto, para qualquer instrução INSERT simultânea, são previstas definições DEFAULT.  
  
 Para obter mais informações, veja [Utilitário bcp](../../tools/bcp-utility.md) e [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql).  
  
### <a name="examples"></a>Exemplos  
 Os exemplos nesta seção efetuam a importação em massa usando **bcp** ou BULK INSERT e mantêm valores nulos.  
  
 A segunda coluna de tabela, **Col2**, tem um valor padrão. O campo correspondente do arquivo de dados contém uma cadeia de caracteres vazia. Por padrão, quando **bcp** ou BULK INSERT é usado para importar dados desse arquivo de dados para a tabela **MyTestDefaultCol2** , o valor padrão de **Col2** é inserido, produzindo o seguinte resultado:  
  
||||  
|-|-|-|  
|`1`|`Default value of Col2`|`DataField3`|  
|`2`|`Default value of Col2`|`DataField3`|  
  
 Para inserir " `NULL` " em vez de " `Default value of Col2` ", você precisa usar a `-k` opção switch ou KEEPNULL, conforme demonstrado nos exemplos de **bcp** e BULK INSERT a seguir.  
  
#### <a name="using-bcp-and-keeping-null-values"></a>Usando bcp e mantendo valores nulos  
 O exemplo a seguir demonstra como manter valores nulos em um comando **bcp** . O comando **bcp** contém as seguintes opções:  
  
|Alternar|Descrição|  
|------------|-----------------|  
|`-f`|Especifica que o comando está usando um arquivo de formato...|  
|`-k`|Especifica que colunas vazias devem reter um valor nulo durante a operação, em vez de qualquer valor padrão nas colunas inseridas.|  
|`-T`|Especifica que o utilitário bcp faz conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de uma conexão confiável.|  
  
 No prompt de comando do Windows, digite:  
  
```  
bcp AdventureWorks..MyTestDefaultCol2 in C:\MyTestEmptyField2-c.Dat -f C:\MyTestDefaultCol2-f-c.Fmt -k -T  
  
```  
  
#### <a name="using-bulk-insert-and-keeping-null-values"></a>Usando BULK INSERT e mantendo valores nulos  
 O exemplo a seguir demonstra como usar a opção KEEPNULLS em uma instrução BULK INSERT. De uma ferramenta de consulta, como o Editor de Consultas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], execute:  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT MyTestDefaultCol2  
   FROM 'C:\MyTestEmptyField2-c.Dat'  
   WITH (  
      DATAFILETYPE = 'char',  
      FIELDTERMINATOR = ',',  
      KEEPNULLS  
   );  
GO  
  
```  
  
## <a name="keeping-default-values-with-insert--select--from-openrowsetbulk"></a>Mantendo valores padrão com INSERT... SELECIONAR * DE OPENROWSET (BULK...)  
 Por padrão, todas as colunas não especificadas na operação de carregamento em massa são definidas como NULL por INSERT... SELECIONE * DE OPENROWSET (BULK...). No entanto, você pode especificar que, para um campo vazio no arquivo de dados, a coluna da tabela correspondente use seu valor padrão (se houver). Para usar valores padrão, especifique a seguinte dica de tabela:  
  
|Comando|Qualificador|Tipo de qualificador|  
|-------------|---------------|--------------------|  
|INSERT ... SELECT * FROM OPENROWSET(BULK...)|WITH(KEEPDEFAULTS)|Dica de tabela|  
  
> [!NOTE]  
>  para obter mais informações, consulte [inserir &#40;&#41;Transact-SQL ](/sql/t-sql/statements/insert-transact-sql), [selecione &#40;&#41;Transact-sql ](/sql/t-sql/queries/select-transact-sql), [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)e [dicas de tabela &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)  
  
### <a name="examples"></a>Exemplos  
 O seguinte inserir... SELECT * do exemplo de OPENROWSET (BULK...) importa dados em massa e mantém os valores padrão.  
  
 Para executar os exemplos, é necessário criar a tabela de exemplo **MyTestDefaultCol2** , o arquivo de dados `MyTestEmptyField2-c.Dat` e usar um arquivo de formato `MyTestDefaultCol2-f-c.Fmt`. Para obter informações sobre como criar esses exemplos, consulte "Tabela e arquivo de dados de exemplo", anteriormente neste tópico.  
  
 A segunda coluna de tabela, **Col2**, tem um valor padrão. O campo correspondente do arquivo de dados contém uma cadeia de caracteres vazia. Quando inserir... SELECIONAR \* de OPENROWSET (bulk...) importar os campos desse arquivo de dados para a tabela **MyTestDefaultCol2** , por padrão, NULL é inserido em **Col2** em vez do valor padrão. Esse comportamento padrão produz o seguinte resultado:  
  
||||  
|-|-|-|  
|`1`|`NULL`|`DataField3`|  
|`2`|`NULL`|`DataField3`|  
  
 Para inserir o valor padrão "`Default value of Col2`" no lugar de "`NULL`" é necessário usar a dica de tabela KEEPDEFAULTS, como demonstrado no exemplo a seguir. De uma ferramenta de consulta, como o Editor de Consultas do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], execute:  
  
```  
USE AdventureWorks;  
GO  
INSERT INTO MyTestDefaultCol2  
    WITH (KEEPDEFAULTS)  
    SELECT *  
      FROM OPENROWSET(BULK  'C:\MyTestEmptyField2-c.Dat',  
      FORMATFILE='C:\MyTestDefaultCol2-f-c.Fmt'       
      ) as t1 ;  
GO  
  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Manter valores de identidade ao importar dados em massa &#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Preparar dados para exportar ou importar em massa &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **Para usar um arquivo de formato**  
  
-   [Criar um arquivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [Usar um arquivo de formato para importação em massa de dados &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **Para usar formatos de dados para importação ou exportação em massa**  
  
-   [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **Para especificar formatos de dados para compatibilidade usando bcp**  
  
-   [Especificar terminadores de campo e linha &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
-   [Especificar o tamanho de prefixo em arquivos de dados usando bcp &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [Especificar tipo de armazenamento de arquivo usando bcp &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [Dicas de tabela &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table)  
  
  
