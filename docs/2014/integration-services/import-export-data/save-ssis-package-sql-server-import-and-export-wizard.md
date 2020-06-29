---
title: Salvar Pacote SSIS (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.savedtspackage.f1
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 690e73e0bda9cac2521cfec3fc6296c50fd3b69a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436803"
---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>Salvar Pacote SSIS (Assistente de Importação e Exportação do SQL Server)
  Use a página **salvar pacote SSIS** para nomear, descrever e salvar um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pacote Integration Services ( [!INCLUDE[ssIS](../../includes/ssis-md.md)] ) no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb` banco de dados ou em um arquivo que tenha a extensão. dtsx.  
  
> [!NOTE]  
>  No [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , a opção para salvar o pacote criado pelo assistente não está disponível.  
  
 Para obter mais informações sobre este assistente, consulte [Assistente de Importação e Exportação do SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções de inicialização do assistente e sobre as permissões necessárias para executar o assistente com êxito, consulte [executar o assistente de importação e exportação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O objetivo do Assistente de Importação e Exportação do SQL Server é copiar dados de uma origem para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **Nome**  
 Forneça um nome exclusivo para o pacote.  
  
 **Descrição**  
 Forneça uma descrição para o pacote. Como prática recomendada, descreva o pacote em termos de objetivo, para facilitar a documentação e a manutenção dos pacotes.  
  
 **Destino**  
 Exiba o destino ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou arquivo) que foi especificado previamente para o arquivo de destino.  
  
## <a name="target-dynamic-options"></a>Opções dinâmicas de destino  
  
### <a name="target--sql-server"></a>Destino = SQL Server  
 **Nome do servidor**  
 Depois de selecionar um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], digite ou selecione o nome do servidor de destino.  
  
 **Usar Autenticação do Windows**  
 Depois de selecionar um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], especifique se deseja se conectar ao servidor usando a Autenticação Integrada do Windows. Esse é o método de autenticação preferido.  
  
 **Usar autenticação SQL Server**  
 Depois de selecionar um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], especifique se deseja se conectar ao servidor usando a Autenticação do SQL Server.  
  
 **Nome de usuário**  
 Depois de selecionar um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e especificar a Autenticação do SQL Server, digite o nome de usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Senha**  
 Depois de selecionar um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e especificar a Autenticação do SQL Server, digite a senha do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="target--file-system"></a>Destino = Sistema de Arquivos  
 **Nome do arquivo**  
 Quando você tiver selecionado um destino de arquivo, digite o caminho para o arquivo de destino ou use o botão **procurar** .  
  
 **Procurar**  
 Quando você tiver selecionado um destino de arquivo, navegue até o arquivo de destino usando a caixa de diálogo **salvar pacote** .  
  
## <a name="see-also"></a>Consulte Também  
 [Salvar pacotes](../save-packages.md)  
  
  
