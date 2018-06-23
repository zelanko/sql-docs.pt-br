---
title: Caixa de diálogo de propriedades, as credenciais da fonte de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.rtp.rptdesigner.datasourceproperties.credentials.f1
- "10100"
ms.assetid: 14c3eeb6-d37b-4fda-967b-43afcdb48119
caps.latest.revision: 38
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: dc168e280f04f43e917c4230e479bd056237e779
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120082"
---
# <a name="data-source-properties-dialog-box-credentials"></a>Caixa de diálogo Propriedades da Fonte de Dados, Credenciais
  Selecione **Credenciais** na caixa de diálogo **Propriedades da Fonte de Dados** para exibir e modificar as credenciais a fim de estabelecer conexão com a fonte de dados no relatório. As credenciais que você fornecer serão usadas para acessar a fonte de dados e para colocar em cache uma cópia dos dados para a visualização dos relatórios. Para obter mais informações sobre como os dados de visualização são armazenados em cache, consulte [Visualizando relatórios](reports/previewing-reports.md). Para obter mais informações sobre credenciais, consulte [Especificar informações de credenciais e de conexão para fontes de dados de relatório](report-data/specify-credential-and-connection-information-for-report-data-sources.md).  
  
## <a name="options"></a>Opções  
 **Usar autenticação do Windows (segurança integrada)**  
 Selecione esta opção para usar a Autenticação do Windows.  
  
 **Usar este nome de usuário e senha**  
 Selecione esta opção para fornecer um nome de usuário e senha específicos. Em fontes de dados compartilhadas: quando você publica o projeto do servidor de relatórios no servidor de destino, o nome de usuário e a senha são salvos como as credenciais armazenadas no banco de dados. Se você quiser usar o nome de usuário e a senha como credenciais do Windows, poderá editar as propriedades da fonte de dados compartilhada no servidor de destino. Para obter mais informações, consulte [Criar, excluir ou modificar uma fonte de dados compartilhada &#40;Gerenciador de Relatórios&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md).  
  
 **Nome de usuário**  
 Digite um nome de usuário para fazer logon na fonte de dados.  
  
 **Senha**  
 Digite uma senha para fazer logon na fonte de dados.  
  
 **Solicitar credenciais**  
 Selecione esta opção para solicitar as credenciais quando o relatório for executado.  
  
 **Insira a cadeia de caracteres de prompt**  
 Digite uma instrução para que o usuário forneça as credenciais de logon para a fonte de dados.  
  
 **Nenhuma credencial**  
 Selecione esta opção para não fornecer nenhuma credencial para a fonte de dados. Esta opção só funcionará se a fonte de dados não aceitar credenciais ou se você estiver passando as credenciais de alguma outra forma.  
  
## <a name="see-also"></a>Consulte também  
 [Caixa de diálogo de propriedades de fonte de dados, geral](../../2014/reporting-services/data-source-properties-dialog-box-general.md)   
 [Especificar informações de credenciais e de conexão para fontes de dados de relatório](report-data/specify-credential-and-connection-information-for-report-data-sources.md)   
 [Conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  