---
title: Usar o formato nativo para importar ou exportar dados (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-bulk-import-export
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- native data format [SQL Server]
- data formats [SQL Server], native
ms.assetid: eb279b2f-0f1f-428f-9b8f-2a7fc495b79f
caps.latest.revision: 40
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 81bfb6671a5c504505de34d368c972de98e21b8a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019384"
---
# <a name="use-native-format-to-import-or-export-data-sql-server"></a>Usar o formato nativo para importar ou exportar dados (SQL Server)
  O formato nativo é recomendado quando você transfere dados em massa entre várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um arquivo de dados que não contém nenhum conjunto de caracteres estendidos ou DBCS (Conjunto de caracteres de byte duplo).  
  
> [!NOTE]  
>  Para transferir dados em massa entre várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um arquivo de dados com caracteres estendidos ou DBCS, use o formato nativo Unicode. Para obter mais informações, veja [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md).  
  
 O formato nativo mantém os tipos de dados nativos de um banco de dados. O formato nativo é planejado para transferência de dados em alta velocidade de dados entre tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você usar um arquivo de formato, as tabelas de origem e destino não precisarão ser idênticas. A transferência de dados envolve duas etapas:  
  
1.  A exportação de dados em massa de uma tabela de origem para um arquivo de dados  
  
2.  A exportação de dados em massa do arquivo de dados para uma tabela de origem  
  
 O uso de formato nativo entre tabelas idênticas evita conversão desnecessária de tipos de dados do e para formato de caractere, economizando tempo e espaço. Porém, para alcançar a taxa de transferência otimizada são executadas algumas verificações referentes à formatação dos dados. Para evitar problemas com os dados carregados, consulte a lista de restrições a seguir.  
  
## <a name="restrictions"></a>Restrictions  
 Para importar dados em formato nativo com êxito, garanta que:  
  
-   O arquivo de dados está em formato nativo.  
  
-   A tabela de destino deve ser compatível com o arquivo de dados (com o número correto de colunas, tipo de dados, comprimento, status NULL, e assim sucessivamente) ou você deve usar um arquivo de formato para mapear cada campo para suas colunas correspondentes.  
  
    > [!NOTE]  
    >  Se você importar dados de um arquivo que não corresponde à tabela de destino, a operação de importação poderá ter sucesso, mas os valores de dados inseridos na tabela de destino poderão estar incorretos. Isso porque os dados do arquivo são interpretados usando o formato da tabela de destino. Portanto, qualquer resultado divergente resultará na inserção de valores incorretos. Porém, em nenhuma circunstância tal divergência pode causar inconsistências lógicas ou físicas no banco de dados.  
  
     Para obter informações sobre como usar arquivos de formato, veja [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
 Uma importação bem-sucedida não corromperá a tabela de destino.  
  
## <a name="how-bcp-handles-data-in-native-format"></a>Como o bcp trata dados no formato nativo  
 Esta seção discute considerações especiais sobre como o utilitário **bcp** exporta e importa dados em formato nativo.  
  
-   Dados não caracteres  
  
     O utilitário bcp usa o formato de dados binário interno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para gravar dados não caracteres de uma tabela para um arquivo de dados.  
  
-   Dados `char` ou `varchar`  
  
     No início de cada `char` ou `varchar` campo, **bcp** adiciona o comprimento do prefixo.  
  
    > [!IMPORTANT]  
    >  Quando o modo nativo é usado, por padrão, o **bcp** utilitário converte caracteres do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em caracteres OEM antes de copiá-los para um arquivo de dados. O **bcp** utilitário converte caracteres de um arquivo de dados em caracteres ANSI antes de importá-los em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela. Durante essas conversões, podem ser perdidos dados de caractere estendidos. Para caracteres estendidos, use o formato nativo Unicode ou especifique uma página de código.  
  
-   `sql_variant` Dados  
  
     Se `sql_variant` dados são armazenados como SQLVARIANT em um arquivo de dados de formato nativo, os dados manterão todas as suas características. Os metadados que registram o tipo de dados de cada valor de dado são armazenados com os valores de dados. Esses metadados são usados para recriar o valor dos dados com o mesmo tipo de dados em um destino `sql_variant` coluna.  
  
     Se o tipo de dados da coluna de destino não é `sql_variant`, cada valor de dados é convertido para o tipo de dados da coluna de destino, seguindo as regras normais de conversão implícita de dados. Se ocorrer um erro durante a conversão dos dados, o lote atual será revertido. Qualquer valor `char` e `varchar` transferido entre colunas `sql_variant` pode ter problemas de conversão de página de código.  
  
     Para obter mais informações sobre conversão de dados, consulte [Conversão de tipo de dados &#40;Mecanismo do Banco de Dados &#41;](/sql/t-sql/data-types/data-type-conversion-database-engine).  
  
## <a name="command-options-for-native-format"></a>Opções de comando para formato nativo  
 Você pode importar dados de formato nativo para uma tabela usando **bcp**, BULK INSERT ou INSERT ... SELECIONE \* DE OPENROWSET(BULK...). Para uma **bcp** comando ou a instrução BULK INSERT, você pode especificar o formato de dados na linha de comando. Para uma instrução INSERT ... instrução SELECT * FROM OPENROWSET(BULK...); é necessário especificar o formato dos dados em um arquivo de formato.  
  
 O formato nativo tem suporte nas seguintes opções de linha de comando:  
  
|Comando|Opção|Description|  
|-------------|------------|-----------------|  
|**bcp**|**-n**|Faz com que o **bcp** utilitário para usar os tipos de dados nativos dos dados.<sup> 1</sup>|  
|BULK INSERT|DATAFILETYPE **='** native **'**|Usa o tipo de dados nativo ou nativo largo. Observe que DATAFILETYPE não será necessário se um arquivo de formato especificar os tipos de dados.|  
  
 <sup>1</sup> carregar nativo (**- n**) dados em um formato compatível com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] clientes, use o **-V** alternar. Para obter mais informações, consulte [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md).  
  
 Para obter mais informações, consulte [Utilitário bcp](../../tools/bcp-utility.md), [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql) ou [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql).  
  
> [!NOTE]  
>  Como alternativa, você pode especificar a formatação por campo, em um arquivo de formato. Para obter mais informações, consulte [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir demonstram como exportar em massa dados nativos com o **bcp** e importar em massa os mesmos dados com BULK INSERT.  
  
### <a name="sample-table"></a>Tabela de exemplo  
 Os exemplos exigem que uma tabela denominada **myTestNativeData** seja criada no banco de dados de exemplo **AdventureWorks** no esquema **dbo**. Antes de executar os exemplos, é necessário criar essa tabela. No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , execute:  
  
```  
USE AdventureWorks;  
GO  
CREATE TABLE myTestNativeData (  
   Col1 smallint,  
   Col2 nvarchar(50),  
   Col3 nvarchar(50)  
   );   
```  
  
 Para preencher esta tabela e exibir o conteúdo resultante, execute as seguintes instruções:  
  
```  
INSERT INTO myTestNativeData(Col1,Col2,Col3)  
   VALUES(1,'DataField2','DataField3');  
INSERT INTO myTestNativeData(Col1,Col2,Col3)  
   VALUES(2,'DataField2','DataField3');  
GO  
SELECT Col1,Col2,Col3 FROM myTestNativeData  
  
```  
  
### <a name="using-bcp-to-bulk-export-native-data"></a>Usando o bcp para exportar dados nativos em massa  
 Para exportar dados da tabela para o arquivo de dados, use **bcp** com a opção **out** e os seguintes qualificadores:  
  
|Qualificadores|Description|  
|----------------|-----------------|  
|**-n**|Especifica tipos de dados nativos.|  
|**-T**|Especifica que o utilitário **bcp** se conecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com uma conexão confiável usando segurança integrada. Se **-T** não for especificado, será necessário especificar **-U** e **-P** para que o logon tenha êxito.|  
  
 O exemplo a seguir exporta dados em massa no formato nativo da tabela `myTestNativeData` para um novo arquivo de dados denominado arquivo de dados `myTestNativeData-n.Dat`. No prompt de comando do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, digite:  
  
```  
bcp AdventureWorks..myTestNativeData out C:\myTestNativeData-n.Dat -n -T  
  
```  
  
### <a name="using-bulk-insert-to-bulk-import-native-data"></a>Usando BULK INSERT para importar dados nativos em massa  
 Os exemplos a seguir usam BULK INSERT para importar os dados no arquivo de dados `myTestNativeData-n.Dat` na tabela `myTestNativeData`. No Editor de Consultas do [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] , execute:  
  
```  
USE AdventureWorks;  
GO  
BULK INSERT myTestNativeData   
    FROM 'C:\myTestNativeData-n.Dat'   
   WITH (DATAFILETYPE='native');   
GO  
SELECT Col1,Col2,Col3 FROM myTestNativeData  
GO  
  
```  
  
##  <a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para usar formatos de dados para importação ou exportação em massa**  
  
-   [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato de caractere Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [sql_variant &#40;Transact-SQL&#41;](/sql/t-sql/data-types/sql-variant-transact-sql)   
 [Importar dados de formato de caractere e nativo de versões anteriores do SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)   
 [Usar o formato nativo Unicode para importar ou exportar dados &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
  
