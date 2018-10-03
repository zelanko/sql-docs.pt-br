---
title: Salvar Pacote SSIS (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.savedtspackage.f1
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8b8ef62839d7379c35b55af7bcb65ab46e4b455d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048227"
---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>Salvar Pacote SSIS (Assistente de Importação e Exportação do SQL Server)
  Use o **salvar pacote SSIS** página para nomear, descrever e salvar um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integration Services ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) do pacote para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb` de banco de dados ou em um arquivo que tenha o dtsx extensão.  
  
> [!NOTE]  
>  No [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], a opção para salvar o pacote criado pelo assistente não está disponível.  
  
 Para saber mais sobre este assistente, consulte [SQL Server Import and Export Wizard](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções para iniciar o assistente e sobre as permissões necessárias para executar o assistente com êxito, consulte [executar o Assistente de exportação e importação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O objetivo do Assistente de Importação e Exportação do SQL Server é copiar dados de uma origem para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **Nome**  
 Forneça um nome exclusivo para o pacote.  
  
 **Descrição**  
 Forneça uma descrição para o pacote. Como prática recomendada, descreva o pacote em termos de objetivo, para facilitar a documentação e a manutenção dos pacotes.  
  
 **Target (destino)**  
 Exiba o destino ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou arquivo) que foi especificado anteriormente para o arquivo de destino.  
  
## <a name="target-dynamic-options"></a>Opções dinâmicas de destino  
  
### <a name="target--sql-server"></a>Destino = SQL Server  
 **Nome do servidor**  
 Depois de selecionar um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], digite ou selecione o nome do servidor de destino.  
  
 **Usar Autenticação do Windows**  
 Depois de selecionar um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], especifique se deseja se conectar ao servidor usando a Autenticação Integrada do Windows. Esse é o método de autenticação preferido.  
  
 **Usar Autenticação do SQL Server**  
 Quando você tiver selecionado um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino, especifique se deseja se conectar ao servidor usando a autenticação do SQL Server.  
  
 **Nome de usuário**  
 Quando você tiver selecionado um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino, e especificar a autenticação do SQL Server, digite o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nome de usuário.  
  
 **Senha**  
 Quando você tiver selecionado um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino, e especificar a autenticação do SQL Server, digite o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] senha.  
  
### <a name="target--file-system"></a>Destino = Sistema de Arquivos  
 **Nome do arquivo**  
 Quando você tiver selecionado um destino de arquivo, digite o caminho para o arquivo de destino ou use o **procurar** botão.  
  
 **Procurar**  
 Quando você tiver selecionado um destino de arquivo, navegue até o arquivo de destino usando o **salvar pacote** caixa de diálogo.  
  
## <a name="see-also"></a>Consulte também  
 [Salvar pacotes](../save-packages.md)  
  
  
