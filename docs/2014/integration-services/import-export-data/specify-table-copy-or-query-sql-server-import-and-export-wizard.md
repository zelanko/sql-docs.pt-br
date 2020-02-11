---
title: Especificar cópia ou consulta de tabela (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.specifytablecopyorquery.f1
ms.assetid: 08aa7158-40e6-4ef3-84d3-1265a8ba194c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 524e878933652699bef6e31da42d3a784b54df7c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62892638"
---
# <a name="specify-table-copy-or-query-sql-server-import-and-export-wizard"></a>Especificar cópia ou consulta de tabela (Assistente de Importação e Exportação do SQL Server)
  Use a página **especificar cópia ou consulta de tabela** para especificar como copiar dados. É possível usar uma interface gráfica para selecionar os objetos existentes do banco de dados que deseja copiar ou usar o Transact-SQL para criar uma consulta mais complexa.  
  
 Para obter mais informações sobre este assistente, consulte [Assistente de Importação e Exportação do SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções de inicialização do assistente, bem como as permissões necessárias para executar o assistente com êxito, consulte [executar o assistente de importação e exportação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O objetivo do Assistente de Importação e Exportação do SQL Server é copiar dados de uma origem para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opções  
 **Copiar dados de uma ou mais tabelas ou exibições**  
 Copie os campos das tabelas de origem e exibições selecionadas para o destino ou os destinos especificados usando a caixa de diálogo **selecionar tabelas e exibições de origem** . Use esta opção para copiar todos os dados na fonte sem filtrar ou ordenar registros.  
  
 Quando você usa um [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] provedor de dados para se conectar à fonte de dados, a opção **copiar dados de uma ou mais tabelas ou exibições** pode não estar disponível. Esta opção só está disponível para os provedores que têm uma seção ProviderDescription no arquivo ProviderDescriptors.xml. Cada seção ProviderDescription contém informações necessárias para recuperar metadados do provedor correspondente. Por padrão, o arquivo ProviderDescriptors.xml contém uma seção ProviderDescription só para os seguintes provedores:  
  
-   System.Data.SqlClient  
  
-   System.Data.OracleClient  
  
-   System.Data.OleDb  
  
-   System.Data.Odbc  
  
 Para tornar a opção **copiar dados de uma ou mais tabelas ou exibições** disponíveis para provedores adicionais, terceiros podem adicionar suas próprias seções ProviderDescriptor ao arquivo arquivo ProviderDescriptors. xml. Por padrão, esse arquivo está na \< *unidade*>: \Program Files\Microsoft SQL Server\100\DTS\ProviderDescriptors. Para verificar as exigências da seção ProviderDescriptor, consulte o arquivo de esquema ProviderDescriptors.xsd que, por padrão, está localizado na mesma pasta do arquivo ProviderDescriptors.xml.  
  
 **Gravar uma consulta para especificar os dados a serem transferidos**  
 Crie instruções SQL para recuperar linhas usando a caixa de diálogo **fornecer uma consulta de origem** . Use essa opção para modificar ou restringir os dados de origem durante a operação de cópia. Só as linhas que correspondem aos critérios de seleção podem ser copiados.  
  
  
