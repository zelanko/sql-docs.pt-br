---
title: Assistente de compilação nativa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
f1_keywords:
- sql12.swb.nativecompilationwizard.f1
- swb.nativecompilationwizard.f1
ms.assetid: d3898a47-2985-4a08-bc70-fd8331a01b7b
author: rothja
ms.author: jroth
ms.openlocfilehash: 175e79f017b795a60088bdaab7939ca51eee9608
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025977"
---
# <a name="native-compilation-advisor"></a>Orientador de compilação nativa
  A ferramenta de relatórios de desempenho da transação (consulte [Determining if a Table or Stored Procedure Should Be Ported to In-Memory OLTP](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)) informa sobre quais procedimentos armazenados interpretados no banco de dados serão beneficiados se usarem a compilação nativa. Depois de identificar um procedimento armazenado que você gostaria de ser aprovado para usar a compilação nativa, você poderá usar o orientador de compilação nativa para ajudá-lo a migrar o procedimento armazenado interpretado para compilação nativa. Para obter mais informações sobre procedimentos armazenados nativamente compilados, consulte [Natively Compiled Stored Procedures](natively-compiled-stored-procedures.md).  
  
 Para começar, conecte-se à instância que contém o procedimento armazenado interpretado. Você pode se conectar a uma instância do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]ou [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] . No entanto, se você desejar executar uma operação de migração com o orientador, deverá se conectar a uma instância do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] na qual a funcionalidade de OLTP na memória está habilitada. Para obter mais informações sobre os requisitos de OLTP na memória, consulte [Requirements for Using Memory-Optimized Tables](memory-optimized-tables.md).  
  
 Para obter informações sobre metodologias de migração, consulte [padrões de carga de trabalho de OLTP em memória e considerações de migração](https://msdn.microsoft.com/library/dn673538.aspx).  
  
## <a name="walkthrough-using-the-native-compilation-advisor"></a>Passo a passo usando o orientador de compilação nativa  
 No **Pesquisador de Objetos**, clique com o botão direito do mouse no procedimento armazenado que você quer converter e selecione **Orientador de Compilação Nativa**. Isso exibirá a página de boas-vindas para o **Orientador de Compilação Nativa de Procedimento Armazenado**. Clique em **Próximo** para continuar.  
  
### <a name="stored-procedure-validation"></a>Validação de procedimento armazenado  
 Essa página relatará se o procedimento armazenado usar alguma construção que não seja compatível com compilação nativa. Você pode clicar em **Avançar** para ver detalhes. Se houver construções que não sejam compatíveis com compilação nativa, você poderá clicar em **Avançar** para ver detalhes.  
  
### <a name="stored-procedure-validation-result"></a>Resultado de validação de procedimento armazenado  
 Se houver construções que não sejam compatíveis com compilação nativa, a página **Resultado de Validação de Procedimento Armazenado** exibirá detalhes. Você pode gerar um relatório (clique em **Gerar Relatório**), saia do **Supervisor de Compilação Nativa**e atualize seu código de forma que seja compatível com a compilação nativa.  
  
## <a name="code-sample"></a>Exemplo de código  
 O exemplo a seguir mostra um procedimento armazenado interpretado e o procedimento armazenado equivalente para compilação nativa. O exemplo supõe um diretório chamado c:\data.  
  
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
GO  
USE Demo;  
GO  
  
CREATE TABLE [dbo].[SalesOrders]  
(  
     [order_id] [int] NOT NULL,  
     [order_date] [datetime] NOT NULL,  
     [order_status] [tinyint] NOT NULL  
  
CONSTRAINT [PK_SalesOrders] PRIMARY KEY NONCLUSTERED HASH   
(  
     [order_id]  
)WITH ( BUCKET_COUNT = 2097152)  
)WITH ( MEMORY_OPTIMIZED = ON )  
  
go  
  
CREATE PROCEDURE [dbo].[InsertOrder] @id INT, @date DATETIME2, @status TINYINT  
AS   
BEGIN   
  
  INSERT dbo.SalesOrders VALUES (@id, @date, @status)  
  
END  
  
go  
  
CREATE PROCEDURE [dbo].[InsertOrderXTP] @id INT, @date DATETIME2, @status TINYINT  
  WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS   
BEGIN ATOMIC WITH   
(    TRANSACTION ISOLATION LEVEL = SNAPSHOT,  
     LANGUAGE = N'us_english')  
  
  INSERT dbo.SalesOrders VALUES (@id, @date, @status)  
  
END  
go  
  
select * from SalesOrders  
go  
exec dbo.InsertOrder @id= 10, @date = '1956-01-01 12:00:00', @status = 1 ;  
exec dbo.InsertOrderXTP @id= 11, @date = '1956-01-01 12:01:00', @status = 2 ;  
select * from SalesOrders  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Migrando para OLTP na memória](migrating-to-in-memory-oltp.md)  
  
  
