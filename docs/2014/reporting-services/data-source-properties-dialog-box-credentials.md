---
title: Caixa de diálogo Propriedades da fonte de dados, credenciais | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.datasourceproperties.credentials.f1
- "10100"
ms.assetid: 14c3eeb6-d37b-4fda-967b-43afcdb48119
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ed5b58aa9a4fe81a55e602fb61f673bf10059ee7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109450"
---
# <a name="data-source-properties-dialog-box-credentials"></a>Caixa de diálogo Propriedades da Fonte de Dados, Credenciais
  Selecione **Credenciais** na caixa de diálogo **Propriedades da Fonte de Dados** para exibir e modificar as credenciais a fim de estabelecer conexão com a fonte de dados no relatório. As credenciais que você fornecer serão usadas para acessar a fonte de dados e para colocar em cache uma cópia dos dados para a visualização dos relatórios. Para obter mais informações sobre como os dados de visualização são armazenados em cache, consulte [Visualizando relatórios](reports/previewing-reports.md). Para obter mais informações sobre credenciais, consulte [Especificar informações de credenciais e de conexão para fontes de dados de relatório](report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
## <a name="options"></a>Opções  
 **Usar a Autenticação do Windows (segurança integrada)**  
 Selecione esta opção para usar a Autenticação do Windows.  
  
 **Usar este nome de usuário e senha**  
 Selecione esta opção para fornecer um nome de usuário e senha específicos. Em fontes de dados compartilhadas: quando você publica o projeto do servidor de relatórios no servidor de destino, o nome de usuário e a senha são salvos como as credenciais armazenadas no banco de dados. Se você quiser usar o nome de usuário e a senha como credenciais do Windows, poderá editar as propriedades da fonte de dados compartilhada no servidor de destino. Para obter mais informações, consulte [Criar, excluir ou modificar uma fonte de dados compartilhada &#40;Gerenciador de Relatórios&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md).  
  
 **Nome de usuário**  
 Digite um nome de usuário para fazer logon na fonte de dados.  
  
 **Senha**  
 Digite uma senha para fazer logon na fonte de dados.  
  
 **Solicita credenciais**  
 Selecione esta opção para solicitar as credenciais quando o relatório for executado.  
  
 **Informar a cadeia de caracteres da solicitação**  
 Digite uma instrução para que o usuário forneça as credenciais de logon para a fonte de dados.  
  
 **Nenhuma credencial**  
 Selecione esta opção para não fornecer nenhuma credencial para a fonte de dados. Esta opção só funcionará se a fonte de dados não aceitar credenciais ou se você estiver passando as credenciais de alguma outra forma.  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo Propriedades da fonte de dados, geral](../../2014/reporting-services/data-source-properties-dialog-box-general.md)   
 [Especificar informações de credencial e de conexão para fontes de dados de relatório](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Data Connections, Data Sources, and Connection Strings in Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  
