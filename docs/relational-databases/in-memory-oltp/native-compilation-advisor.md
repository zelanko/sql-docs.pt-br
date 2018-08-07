---
title: Assistente de compilação nativa | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.nativecompilationwizard.f1
- swb.nativecompilationwizard.f1
ms.assetid: d3898a47-2985-4a08-bc70-fd8331a01b7b
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 201c7ac4f933a852fcdc019b1da596a89f6d0960
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39546279"
---
# <a name="native-compilation-advisor"></a>Orientador de compilação nativa
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Os relatórios de Análise de desempenho de transação informa sobre quais procedimentos armazenados interpretados no banco de dados serão beneficiados se usarem a compilação nativa. Para obter detalhes, veja [Determinando se uma tabela ou um procedimento armazenado deve ser movido para o OLTP in-memory](../../relational-databases/in-memory-oltp/determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md).  
  
 Depois de identificar um procedimento armazenado que você gostaria de ser aprovado para usar a compilação nativa, você pode usar o NCA (Native Compilation Advisor) para ajudar com a migração do procedimento armazenado interpretado para compilação nativa. Para obter mais informações sobre procedimentos armazenados nativamente compilados, consulte [Natively Compiled Stored Procedures](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
 Em um determinado procedimento armazenado interpretado, o NCA permite a identificação de todos os recursos que não têm suporte em módulos nativos. O NCA fornece links de documentação para soluções ou soluções alternativas.  
  
 Para obter informações sobre as metodologias de migração, consulte [In-Memory OLTP – Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx)(OLTP in-memory – Padrões comuns de carga de trabalho e considerações de migração).  
  
## <a name="walkthrough-using-the-native-compilation-advisor"></a>Passo a passo usando o orientador de compilação nativa  
 No **Pesquisador de Objetos**, clique com o botão direito do mouse no procedimento armazenado que você quer converter e selecione **Orientador de Compilação Nativa**. Isso exibirá a página de boas-vindas para o **Orientador de Compilação Nativa de Procedimento Armazenado**. Clique em **Avançar** para continuar.  
  
### <a name="stored-procedure-validation"></a>Validação de procedimento armazenado  
 Essa página relatará se o procedimento armazenado usar alguma construção que não seja compatível com compilação nativa. Você pode clicar em **Avançar** para ver detalhes. Se houver construções que não sejam compatíveis com compilação nativa, você poderá clicar em **Avançar** para ver detalhes.  
  
### <a name="stored-procedure-validation-result"></a>Resultado de validação de procedimento armazenado  
 Se houver construções que não sejam compatíveis com compilação nativa, a página **Resultado de Validação de Procedimento Armazenado** exibirá detalhes. Você pode gerar um relatório (clique em **Gerar Relatório**), saia do **Supervisor de Compilação Nativa**e atualize seu código de forma que seja compatível com a compilação nativa.  
  
## <a name="code-sample"></a>Exemplo de código  
 O exemplo a seguir mostra um procedimento armazenado interpretado e o procedimento armazenado *equivalente* para compilação nativa. O exemplo supõe um diretório chamado c:\data.  
  
> [!NOTE]  
>  Como de costume, o elemento **FILEGROUP** e a instrução mydatabase **USE** se aplicam ao Microsoft SQL Server, mas não ao Banco de Dados SQL do Azure.  
  
```sql  
CREATE DATABASE Demo  
ON  
PRIMARY(NAME = [Demo_data],  
FILENAME = 'C:\DATA\Demo_data.mdf', size=500MB)  
, FILEGROUP [Demo_fg] CONTAINS MEMORY_OPTIMIZED_DATA(  
NAME = [Demo_dir],  
FILENAME = 'C:\DATA\Demo_dir')  
LOG ON (name = [Demo_log], Filename='C:\DATA\Demo_log.ldf', size=500MB)  
COLLATE Latin1_General_100_BIN2;  
go  
  
USE Demo;  
go  
  
CREATE TABLE [dbo].[SalesOrders]  
(  
     [order_id] [int] NOT NULL,  
     [order_date] [datetime] NOT NULL,  
     [order_status] [tinyint] NOT NULL  
     CONSTRAINT [PK_SalesOrders] PRIMARY KEY NONCLUSTERED HASH   
(  
     [order_id]  
) WITH ( BUCKET_COUNT = 2097152)  
) WITH ( MEMORY_OPTIMIZED = ON )  
go  
  
-- Interpreted.  
CREATE PROCEDURE [dbo].[InsertOrder] @id INT, @date DATETIME2, @status TINYINT  
AS   
BEGIN   
  INSERT dbo.SalesOrders VALUES (@id, @date, @status);  
END  
go  
  
-- Natively Compiled.  
CREATE PROCEDURE [dbo].[InsertOrderXTP]  
      @id INT, @date DATETIME2, @status TINYINT  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS   
BEGIN ATOMIC WITH   
     (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
     )  
  INSERT dbo.SalesOrders VALUES (@id, @date, @status);  
END  
go  
  
SELECT * from SalesOrders;  
go  
  
EXECUTE dbo.InsertOrder @id= 10, @date = '1956-01-01 12:00:00', @status = 1;  
EXECUTE dbo.InsertOrderXTP @id= 11, @date = '1956-01-01 12:01:00', @status = 2;  
  
SELECT * from SalesOrders;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Migrando para OLTP na memória](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)   
 [Requisitos para usar tabelas com otimização de memória](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)  
  
  
