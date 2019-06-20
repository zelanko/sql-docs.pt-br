---
title: Usar o formato de caractere para importar ou exportar dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- data formats [SQL Server], character
- character formats [SQL Server]
ms.assetid: d925e66a-1a73-43cd-bc06-1cbdf8174a4d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ab658be26dc8ccbdd4e760d0b1bc835ace3b2c38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011664"
---
# <a name="use-character-format-to-import-or-export-data-sql-server"></a>Usar o formato de caractere para importar ou exportar dados (SQL Server)
  Formato de caractere é recomendado quando você exporta dados em massa para um arquivo de texto que será usado em outro programa ou quando você importa dados em massa de um arquivo de texto que é gerado por outro programa.  
  
> [!NOTE]  
>  Quando você transfere dados em massa entre instâncias do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o arquivo de dados contém dados de caractere Unicode mas não caracteres estendidos ou DBCS, use o formato de caractere Unicode. Para obter mais informações, consulte [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md).  
  
 Formato de caractere usa o formato de dados de caractere para todas as colunas. Armazenar informações em formato de caractere é útil quando os dados são usados com outro programa, como uma planilha, ou quando os dados precisam ser copiados em uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de outro fornecedor de banco de dados como Oracle.  
  
## <a name="considerations-for-using-character-format"></a>Considerações sobre usar o formato de caractere  
 Ao usar formato de caractere, considere o seguinte:  
  
-   Por padrão, o utilitário **bcp** separa os campos dos dados de caractere com o caractere de guia e termina os registros com o caractere de nova linha. Para obter informações sobre como especificar terminadores alternativos, consulte [Especificar terminadores de campo e linha &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md).  
  
-   Por padrão, antes da exportação ou importação em massa de dados do modo de caractere, são executadas as conversões seguintes:  
  
    |Direção da operação em massa|Conversão|  
    |---------------------------------|----------------|  
    |Exportar|Converte dados para representação de caractere. Se solicitado explicitamente, os dados são convertidos à página de código solicitada para colunas de caractere. Se nenhuma página de código for especificada, os dados de caractere serão convertidos usando a página de código OEM do computador do cliente.|  
    |Importar|Converte dados de caractere em representação nativa e traduz os dados de caractere da página de código do cliente para a página de código da(s) coluna(s) de destino, quando necessário.|  
  
-   Para evitar a perda de caracteres estendidos durante conversão, use formato de caractere Unicode ou especifique uma página de código.  
  
-   São armazenados quaisquer dados `sql_variant` em um arquivo do formato de caractere sem metadados. Cada valor de dados é convertido ao formato `char`, de acordo com as regras de conversão de dados implícita. Quando importado em uma coluna `sql_variant`, os dados são importados como `char`. Quando importado em uma coluna com um tipo de dados diferente de `sql_variant`, os dados são convertidos de `char` usando conversão implícita. Para obter mais informações sobre conversão de dados, consulte [Conversão de tipo de dados &#40;Mecanismo do Banco de Dados &#41;](/sql/t-sql/data-types/data-type-conversion-database-engine).  
  
-   O **bcp** exportações de utilitário `money` valores como arquivos de dados de formato de caractere com quatro dígitos após o ponto decimal e sem qualquer símbolo de agrupamento de dígito como separadores de vírgula. Por exemplo, uma coluna `money` que contém o valor 1,234,567.123456 é exportado em massa para um arquivo de dados como a cadeia de caracteres 1234567.1235.  
  
## <a name="command-options-for-character-format"></a>Opções de comando para formato de caractere  
 Você pode importar dados de formato de caractere em uma tabela que usa **bcp**, BULK INSERT ou INSERT ... SELECIONE \* DE OPENROWSET. Para um comando **bcp** ou uma instrução BULK INSERT, você pode especificar o formato de dados na linha de comando. Para uma instrução INSERT ... instrução SELECT * FROM OPENROWSET(BULK...); é necessário especificar o formato dos dados em um arquivo de formato.  
  
 O formato de caractere tem suporte nas seguintes opções de linha de comando:  
  
|Comando|Opção|Descrição|  
|-------------|------------|-----------------|  
|**bcp**|**-c**|Faz com que o **bcp** utilitário use dados de caractere.<sup> 1</sup>|  
|BULK INSERT|DATAFILETYPE **='char'**|Use o formato de caractere quando na importação em massa de dados.|  
  
 <sup>1</sup> para carregar caractere ( **- c**) dados em um formato compatível com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] clientes, use o **-V** alternar. Para obter mais informações, consulte [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md).  
  
 Para obter mais informações, consulte [Utilitário bcp](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) ou [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
> [!NOTE]  
>  Como alternativa, você pode especificar a formatação por campo, em um arquivo de formato. Para obter mais informações, consulte [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir demonstram como exportar dados de caractere em massa usando **bcp** e importar os mesmos dados em massa usando BULK INSERT.  
  
### <a name="sample-table"></a>Tabela de exemplo  
 Os exemplos requerem que uma tabela denominada **myTestCharData** seja criada no banco de dados de exemplo **AdventureWorks** no esquema **dbo**. Antes de executar os exemplos, é necessário criar essa tabela. Para criar essa tabela, no Editor de Consultas do SQL[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], execute:  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestCharData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 Para preencher esta tabela e exibir o conteúdo resultante, execute as seguintes instruções:  
  
```  
INSERT INTO myTestCharData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestCharData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestCharData  
  
```  
  
### <a name="using-bcp-to-bulk-export-character-data"></a>Usando o bcp para exportar em massa dados de caractere  
 Para exportar dados da tabela para o arquivo de dados, use **bcp** com a opção **out** e os seguintes qualificadores:  
  
|Qualificadores|Descrição|  
|----------------|-----------------|  
|**-c**|Especifica o formato do caractere.|  
|**-t** `,`|Especifica uma vírgula (`,`) como terminador de campo.<br /><br /> Observação: O terminador de campo padrão é o caractere de tabulação (\t). Para obter mais informações, veja [Especificar terminadores de campo e linha &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md).|  
|**-T**|Especifica que o utilitário **bcp** se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com uma conexão confiável usando segurança integrada. Se **-T** não for especificado, será necessário especificar **-U** e **-P** para que o logon tenha êxito.|  
  
 O exemplo seguinte exporta em massa dados em formato de caractere da tabela `myTestCharData` em um arquivo de dados novo nomeado arquivo de dados `myTestCharData-c.Dat` que usa a vírgula (,) como terminador de campo. No prompt de comando do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, digite:  
  
```  
bcp AdventureWorks..myTestCharData out C:\myTestCharData-c.Dat -c -t, -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-character-data"></a>Usando BULK INSERT para importar dados de caractere em massa  
 Os exemplos a seguir usam BULK INSERT para importar os dados no arquivo de dados `myTestCharData-c.Dat` na tabela `myTestCharData`. No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , execute:  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestCharData   
   FROM 'C:\myTestCharData-c.Dat'   
   WITH (  
      DATAFILETYPE='char',  
      FIELDTERMINATOR=','  
   );   
GO  
SELECT Col1,Col2,Col3 FROM myTestCharData;  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para usar formatos de dados para importação ou exportação em massa**  
  
-   [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
  
