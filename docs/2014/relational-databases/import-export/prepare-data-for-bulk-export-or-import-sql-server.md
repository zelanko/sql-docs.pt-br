---
title: Preparar dados para exportação ou importação em massa (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk importing [SQL Server], planning
- bulk importing [SQL Server], from a CSV file
- data formats [SQL Server], planning operations
- CSV files [SQL Server]
- quoted fields in CSV files [SQL Server]
ms.assetid: 783fd581-2e5f-496b-b79c-d4de1e09ea30
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d0836d835b77241a27dfccc65528e8cda440559c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62519280"
---
# <a name="prepare-data-for-bulk-export-or-import-sql-server"></a>Preparar dados para exportar ou importar em massa (SQL Server)
  Esta seção descreve as considerações envolvidas no planejamento de operações de exportação em massa e os requisitos para operações de importação em massa.  
  
> [!NOTE]  
>  Se não tiver certeza de como formatar um arquivo de dados para a importação em massa, você poderá usar o utilitário **bcp** para exportar dados da tabela para um arquivo de dados. A formatação de cada campo de dados neste arquivo mostra a formatação necessária para importar dados em massa na coluna da tabela correspondente. Use a mesma formatação de dados para os campos do arquivo de dados.  
  
## <a name="data-file-format-considerations-for-bulk-export"></a>Considerações de formato de arquivo de dados para exportação em massa  
 Antes de executar uma operação da exportação em massa usando o comando **bcp** , considere o seguinte:  
  
-   Quando dados são exportados para um arquivo, o comando **bcp** cria o arquivo de dados automaticamente usando o nome de arquivo especificado. Se esse nome de arquivo já estiver em uso, os dados que estão sendo copiados em massa para o arquivo de dados substituirão o conteúdo existente no arquivo.  
  
-   A exportação em massa de uma tabela ou exibição para um arquivo de dados requer permissão SELECT na tabela ou exibição que estiver sendo copiada em massa.  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode usar exames paralelos para recuperar dados. Portanto, as linhas de tabela que são exportadas em massa de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não têm a garantia de estar em qualquer ordem específica no arquivo de dados. Para garantir que as linhas de tabela exportadas em massa apareçam em uma ordem específica no arquivo de dados, use a opção **queryout** para exportar em massa de uma consulta e especifique uma cláusula ORDER BY.  
  
## <a name="data-file-format-requirements-for-bulk-import"></a>Requisitos de formato de arquivo de dados para importação em massa  
 Para importar dados de um arquivo de dados, o arquivo deve atender os seguintes requisitos básicos:  
  
-   Os dados devem estar em formato de linha e coluna.  
  
> [!NOTE]  
>  A estrutura do arquivo de dados não precisa ser idêntica à estrutura da tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , porque colunas podem ser ignoradas ou reordenadas durante o processo de importação em massa.  
  
-   Os dados no arquivo de dados devem estar em um formato suportado como formato de caractere ou nativo.  
  
-   Os dados podem estar em formato de caractere ou binário nativo, inclusive Unicode.  
  
-   Para importar dados usando um comando **bcp**, use a instrução BULK INSERT ou INSERT... SELECT * FROM OPENROWSET(BULK...); a tabela de destino já deve existir.  
  
-   Cada campo no arquivo de dados deve ser compatível com a coluna correspondente na tabela de destino. Por exemplo, um campo `int` não pode ser carregado em uma coluna `datetime`. Para obter mais informações, consulte [Data Formats for Bulk Import or Bulk Export &#40;SQL Server&#41;](data-formats-for-bulk-import-or-bulk-export-sql-server.md) [Formatos de dados para importação ou exportação em massa (SQL Server)] e [Especificar formatos de dados para compatibilidade usando bcp &#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).  
  
    > [!NOTE]  
    >  Para especificar um subconjunto de linhas para importar de um arquivo de dados em vez do arquivo inteiro, você pode usar um comando **bcp** com a opção **-F** *first_row* e/ou **-L** *last_row*. Para obter mais informações, consulte [bcp Utility](../../tools/bcp-utility.md).  
  
-   Para importar dados de arquivos de dados com campos de comprimento ou de largura fixos, você deve usar um arquivo de formato. Para obter mais informações, veja [Arquivos de formato XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  
-   Arquivos CSV (valores separados por vírgula) não têm suporte das operações de importação em massa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No entanto, em alguns casos, um arquivo CSV pode ser usado como o arquivo de dados para uma importação em massa de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Observe que o terminador de campo de um arquivo CSV não tem que ser uma vírgula. Para ser usável como um arquivo de dados para importação em massa, um arquivo de CSV deve obedecer as seguintes restrições:  
  
    -   Campos de dados nunca contêm o terminador de campo.  
  
    -   Nenhum ou todos os valores em um campo de dados estão inclusos entre aspas ("").  
  
     Para dados de importação em massa de um arquivo (.dbf) de tabela FoxPro ou Visual FoxPro do [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou de um arquivo de planilha (.xls) do [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] , você precisa converter os dados em um arquivo CSV, compatível com as restrições anteriores. A extensão de arquivo normalmente é .csv. Portanto, você pode usar o arquivo .csv como um arquivo de dados em uma operação de importação em massa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Em sistemas de 32 bits, é possível importar dados de CSV em uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sem otimizações de importação em massa usando [OPENROWSET](/sql/t-sql/functions/openrowset-transact-sql) com o Provedor do OLE DB para Jet. O Jet trata arquivos de texto como tabelas, com o esquema definido por um arquivo schema.ini localizado no mesmo diretório da fonte de dados.  Para dados CSV, um dos parâmetros no arquivo schema.ini é "FORMAT=CSVDelimited". Para usar essa solução, você precisa compreender as operações do Jet Test IISAMm (sua sintaxe de cadeia de conexão, o uso de schema.ini, as opções de configuração do Registro e assim por diante).  As melhores fontes dessas informações são a Ajuda do Microsoft Access e artigos da Base de Conhecimentos (KB). Para obter mais informações, consulte [Inicializando o Driver de fonte de dados de texto](https://go.microsoft.com/fwlink/?LinkId=128503), [como usar uma consulta distribuída do SQL Server 7.0 com um servidor vinculado para bancos de dados protegidos](https://go.microsoft.com/fwlink/?LinkId=128504), [HOW TO: Usar o provedor OLE DB Jet 4.0 para se conectar aos bancos de dados ISAM](https://go.microsoft.com/fwlink/?LinkId=128505), e [como abrir arquivos de texto delimitados usando texto IIsam do provedor de Jet](https://go.microsoft.com/fwlink/?LinkId=128501).  
  
 Além disso, a importação em massa de dados de um arquivo de dados para uma tabela exige o seguinte:  
  
-   Usuários devem ter permissões INSERT e SELECT na tabela. Os usuários também precisam de permissão ALTER TABLE quando usarem opções que requerem operações de DDL (linguagem de definição de dados), como desabilitar restrições.  
  
-   Ao importar dados em massa usando BULK INSERT ou INSERT... SELECT * FROM OPENROWSET(BULK...), o arquivo de dados deve estar acessível para operações de leitura pelo perfil de segurança do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (se o usuário fizer logon usando o logon fornecido pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) ou pelo logon do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows que é usado sob segurança delegada. Além disso, o usuário deve ter permissão de ADMINISTER BULK OPERATIONS para ler o arquivo.  
  
> [!NOTE]  
>  Não há suporte para a importação em massa de uma exibição particionada; tentativas de fazer importação de dados em massa em uma visão particionada falharão.  
  
## <a name="external-resources"></a>Recursos externos  
 [Como importar dados do Excel para o SQL Server](https://support.microsoft.com/kb/321686)  
  
## <a name="change-history"></a>Histórico de alterações  
  
|Conteúdo atualizado|  
|---------------------|  
|Informações complementares sobre como usar o Provedor OLE DB para Jet para importar dados CSV.|  
  
## <a name="see-also"></a>Consulte também  
 [bcp Utility](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Usar o formato de caractere para importar ou exportar dados &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)   
 [Usar o formato nativo para importar ou exportar dados &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
  
