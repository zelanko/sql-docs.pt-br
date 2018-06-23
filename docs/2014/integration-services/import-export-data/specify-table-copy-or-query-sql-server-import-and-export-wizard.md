---
title: Especificar cópia ou consulta de tabela (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.impexpwizard.specifytablecopyorquery.f1
ms.assetid: 08aa7158-40e6-4ef3-84d3-1265a8ba194c
caps.latest.revision: 43
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 413dd857be0ab913f43bd07f9c2f82d536137dad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012940"
---
# <a name="specify-table-copy-or-query-sql-server-import-and-export-wizard"></a>Especificar cópia ou consulta de tabela (Assistente de Importação e Exportação do SQL Server)
  Use o **especificar cópia da tabela ou consulta** página para especificar como copiar dados. É possível usar uma interface gráfica para selecionar os objetos existentes do banco de dados que deseja copiar ou usar o Transact-SQL para criar uma consulta mais complexa.  
  
 Para saber mais sobre este assistente, consulte [SQL Server Import and Export Wizard](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções para iniciar o assistente, bem como as permissões necessárias para executar o assistente com êxito, consulte [executar o Assistente de exportação e importação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O objetivo do Assistente de Importação e Exportação do SQL Server é copiar dados de uma origem para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opções  
 **Copiar dados de uma ou mais tabelas ou exibições**  
 Copiar os campos de tabelas de origem selecionado e modos de exibição para o destino especificado ou destinos usando o **selecionar tabelas de origem e exibições** caixa de diálogo. Use esta opção para copiar todos os dados na fonte sem filtrar ou ordenar registros.  
  
 Quando você usa um [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] provedor de dados para se conectar à fonte de dados, o **copiar dados de uma ou mais tabelas ou exibições** opção pode não estar disponível. Esta opção só está disponível para os provedores que têm uma seção ProviderDescription no arquivo ProviderDescriptors.xml. Cada seção ProviderDescription contém informações necessárias para recuperar metadados do provedor correspondente. Por padrão, o arquivo ProviderDescriptors.xml contém uma seção ProviderDescription só para os seguintes provedores:  
  
-   System.Data.SqlClient  
  
-   System.Data.OracleClient  
  
-   System.Data.OleDb  
  
-   System.Data.Odbc  
  
 Para fazer o **copiar dados de uma ou mais tabelas ou exibições** opção disponível para provedores adicionais, terceiros podem adicionar suas próprias seções ProviderDescriptor ao arquivo ProviderDescriptors.xml. Por padrão, esse arquivo está em \< *unidade*>: \Program Files\Microsoft Server\100\DTS\ProviderDescriptors SQL. Para verificar as exigências da seção ProviderDescriptor, consulte o arquivo de esquema ProviderDescriptors.xsd que, por padrão, está localizado na mesma pasta do arquivo ProviderDescriptors.xml.  
  
 **Gravar uma consulta para especificar os dados a serem transferidos**  
 Construa instruções SQL para recuperar linhas usando o **fornecer uma consulta de origem** caixa de diálogo. Use essa opção para modificar ou restringir os dados de origem durante a operação de cópia. Só as linhas que correspondem aos critérios de seleção podem ser copiados.  
  
  