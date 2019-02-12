---
title: Propriedades do servidor (página Segurança) – Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.security.f1
ms.assetid: f49aedc6-f145-4df1-8f69-d5d910f492c6
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 89d8b7165bf32d4d4d300f753b9c3821b6f23134
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041167"
---
# <a name="server-properties-security-page---reporting-services"></a>Propriedades do Servidor (página Segurança) - Reporting Services
  Use esta página para desativar recursos que podem comprometer um servidor de relatório potencialmente. A desativação desse recurso limitará algumas funcionalidades, mas pode aprimorar a segurança geral do servidor de relatório, reduzindo ameaças específicas.  
  
 Para abrir essa página, inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a uma instância de servidor de relatórios, clique com o botão direito do mouse no nome do servidor de relatórios e selecione **Propriedades**. Clique em **Segurança** para abrir essa página.  
  
## <a name="options"></a>Opções  
 **Habilitar a segurança integrada do Windows para as fontes de dados do relatório**  
 Especifique se uma conexão com uma fonte de dados de relatório pode ser feita usando o token de segurança do Windows do usuário que solicitou o relatório.  
  
 Se esse recurso for desativado, o recurso de Segurança Integrada do Windows nas páginas de propriedades das fontes de dados do relatório se tornará indisponível. Se as fontes de dados do relatório estiverem configuradas para segurança integrada do Windows e você subsequentemente desativar esse recurso, o servidor de relatório atualizará imediatamente todas as propriedades de conexão da fonte de dados para solicitar credenciais.  
  
 **Habilitar Relatórios Ad Hoc**  
 Especifique se os usuários podem executar consultas ad hoc de um relatório do Construtor de Relatórios, onde novos relatórios são automaticamente gerados quando um usuário clica nos dados de interesse.  
  
 A definição dessa opção determina se a propriedade `EnableLoadReportDefinition` no servidor de relatório é definida como `True` ou `False`. Se você desmarcar esta opção, a propriedade será definida como `False` e o servidor de relatório não gerará relatórios de clickthrough criados durante a exploração dos dados. Todas as chamadas para o método `LoadReportDefinition` serão bloqueadas.  
  
 A desativação dessa opção reduz uma ameaça de que um usuário mal-intencionado inicie um ataque de negação de serviço, sobrecarregando o servidor de relatório com solicitações `LoadReportDefinition`.  
  
## <a name="see-also"></a>Consulte também  
 [Definir propriedades do servidor de relatório &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Conectar-se a um servidor de relatório no Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Especificar credenciais e informações de Conexão para fontes de dados de relatórios] (.. /Report-Data/Specify-Credential-and-Connection-Information-for-Report-Data-Sources.MD [servidor de relatório na Ajuda de F1 do Management Studio](report-server-in-management-studio-f1-help.md)  
  
  
