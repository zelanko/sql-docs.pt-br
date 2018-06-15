---
title: Preparar dados para exportação ou importação em massa (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: import-export
ms.reviewer: ''
ms.suite: sql
ms.technology: data-movement
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], planning
- bulk importing [SQL Server], from a CSV file
- data formats [SQL Server], planning operations
- CSV files [SQL Server]
- quoted fields in CSV files [SQL Server]
ms.assetid: 783fd581-2e5f-496b-b79c-d4de1e09ea30
caps.latest.revision: 52
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b721a608a256c0416cd2bb00426ed947d88a9862
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32939461"
---
# <a name="prepare-data-for-bulk-export-or-import-sql-server"></a>Preparar dados para exportar ou importar em massa (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Esta seção descreve as considerações envolvidas no planejamento de operações de exportação em massa e os requisitos para operações de importação em massa.  
  
> [!NOTE]  
>  Se não tiver certeza de como formatar um arquivo de dados para a importação em massa, use o utilitário **bcp** para exportar dados da tabela para um arquivo de dados. A formatação de cada campo de dados neste arquivo mostra a formatação necessária para importar dados em massa na coluna da tabela correspondente. Use a mesma formatação de dados para os campos do arquivo de dados.  
  
## <a name="data-file-format-considerations-for-bulk-export"></a>Considerações de formato de arquivo de dados para exportação em massa  
 Antes de executar uma operação da exportação em massa usando o comando **bcp** , considere o seguinte:  
  
-   Quando dados são exportados para um arquivo, o comando **bcp** cria o arquivo de dados automaticamente usando o nome de arquivo especificado. Se esse nome de arquivo já estiver em uso, os dados que estão sendo copiados em massa para o arquivo de dados substituirão o conteúdo existente no arquivo.  
  
-   A exportação em massa de uma tabela ou exibição para um arquivo de dados requer permissão SELECT na tabela ou exibição que estiver sendo copiada em massa.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode usar exames paralelos para recuperar dados. Portanto, as linhas de tabela que são exportadas em massa de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não têm a garantia de estar em qualquer ordem específica no arquivo de dados. Para mostrar as linhas de tabela exportadas em massa em uma ordem específica no arquivo de dados, use a opção **queryout** para exportar em massa de uma consulta e especifique uma cláusula ORDER BY.  
  
## <a name="data-file-format-requirements-for-bulk-import"></a>Requisitos de formato de arquivo de dados para importação em massa  
 Para importar dados de um arquivo de dados, o arquivo deve atender os seguintes requisitos básicos:  
  
-   Os dados devem estar em formato de linha e coluna.  
  
> [!NOTE]  
>  A estrutura do arquivo de dados não precisa ser idêntica à estrutura da tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , porque colunas podem ser ignoradas ou reordenadas durante o processo de importação em massa.  
  
-   Os dados no arquivo de dados devem estar em um formato suportado como formato de caractere ou nativo.  
  
-   Os dados podem estar em formato de caractere ou binário nativo, inclusive Unicode.  
  
-   Para importar dados usando um comando **bcp**, use a instrução BULK INSERT ou INSERT... SELECT * FROM OPENROWSET(BULK...); a tabela de destino já deve existir.  
  
-   Cada campo no arquivo de dados deve ser compatível com a coluna correspondente na tabela de destino. Por exemplo, um campo **int** não pode ser carregado em uma coluna **datetime** . Para obter mais informações, consulte [Data Formats for Bulk Import or Bulk Export &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md) [Formatos de dados para importação ou exportação em massa (SQL Server)] e [Especificar formatos de dados para compatibilidade usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).  
  
    > [!NOTE]  
    >  Para especificar um subconjunto de linhas para importar de um arquivo de dados em vez do arquivo inteiro, você pode usar um comando **bcp** com a opção **-F** *first_row* e/ou **-L** *last_row*. Para obter mais informações, consulte [bcp Utility](../../tools/bcp-utility.md).  
  
-   Para importar dados de arquivos de dados com campos de comprimento ou de largura fixos, use um arquivo de formato. Para obter mais informações, veja [Arquivos de formato XML &#40;SQL Server&#41;](../../relational-databases/import-export/xml-format-files-sql-server.md).  
  
-   Arquivos CSV (valores separados por vírgula) não têm suporte das operações de importação em massa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No entanto, em alguns casos, um arquivo CSV pode ser usado como o arquivo de dados para uma importação em massa de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Observe que o terminador de campo de um arquivo CSV não tem que ser uma vírgula. Para ser usável como um arquivo de dados para importação em massa, um arquivo de CSV deve obedecer as seguintes restrições:  
  
    -   Campos de dados nunca contêm o terminador de campo.  
  
    -   Nenhum ou todos os valores em um campo de dados estão inclusos entre aspas ("").  
  
     Para dados de importação em massa de um arquivo (.dbf) de tabela FoxPro ou Visual FoxPro do [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou de um arquivo de planilha (.xls) do [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] , você precisa converter os dados em um arquivo CSV, compatível com as restrições anteriores. A extensão de arquivo normalmente é .csv. Portanto, você pode usar o arquivo .csv como um arquivo de dados em uma operação de importação em massa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Em sistemas de 32 bits, é possível importar dados de CSV em uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem otimizações de importação em massa usando [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) com o Provedor do OLE DB para Jet. O Jet trata arquivos de texto como tabelas, com o esquema definido por um arquivo schema.ini localizado no mesmo diretório da fonte de dados.  Para dados CSV, um dos parâmetros no arquivo schema.ini é "FORMAT=CSVDelimited". Para usar essa solução, você precisa compreender as operações do Jet Test IISAMm (sua sintaxe de cadeia de conexão, o uso de schema.ini, as opções de configuração de Registro, e assim por diante).  As melhores fontes dessas informações são a Ajuda do Microsoft Access e artigos da Base de Conhecimentos (KB). Para obter mais informações, consulte [Inicializando o driver da fonte de dados de texto](https://msdn.microsoft.com/library/office/ff834391.aspx), [Como usar uma consulta distribuída do SQL Server 7.0 com um servidor vinculado aos bancos de dados de acesso protegidos](http://go.microsoft.com/fwlink/?LinkId=128504), [COMO usar o Jet OLE DB Provider 4.0 para conectar aos bancos de dados ISAM](http://go.microsoft.com/fwlink/?LinkId=128505)e [Como abrir arquivos de texto delimitados usando o Text II sam do Jet Provider](http://go.microsoft.com/fwlink/?LinkId=128501).  
  
 Além disso, a importação em massa de dados de um arquivo de dados para uma tabela exige o seguinte:  
  
-   Usuários devem ter permissões INSERT e SELECT na tabela. Os usuários também precisam de permissão ALTER TABLE quando usarem opções que requerem operações de DDL (linguagem de definição de dados), como desabilitar restrições.  
  
-   Ao importar dados em massa usando BULK INSERT ou INSERT... SELECT * FROM OPENROWSET(BULK...), o arquivo de dados deve estar acessível para operações de leitura pelo perfil de segurança do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (se o usuário fizer logon usando o logon fornecido pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) ou pelo logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows que é usado sob segurança delegada. Além disso, o usuário deve ter permissão de ADMINISTER BULK OPERATIONS para ler o arquivo.  
  
> [!NOTE]  
>  Não há suporte para a importação em massa de uma exibição particionada; tentativas de fazer importação de dados em massa em uma visão particionada falharão.  
  
## <a name="external-resources"></a>Recursos externos  
 [Como importar dados do Excel para o SQL Server](http://support.microsoft.com/kb/321686)  
  
## <a name="change-history"></a>Histórico de alterações  
  
|Conteúdo atualizado|  
|---------------------|  
|Informações complementares sobre como usar o Provedor OLE DB para Jet para importar dados CSV.|  
  
## <a name="see-also"></a>Consulte Também  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)   
 [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)  
  
  
