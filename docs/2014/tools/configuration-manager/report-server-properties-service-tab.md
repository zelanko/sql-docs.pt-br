---
title: Propriedades do servidor de relatório (guia Serviço) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 2a2e1dbf-02b9-4893-aaf0-c0e4a2c9b4f9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ef0f55049e5ae9c96eed10fb1f39d7f3d95a19f9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62506768"
---
# <a name="report-server-properties-service-tab"></a>Propriedades do servidor de relatório (guia Serviço)
  Esse serviço é o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço servidor de relatório. Os valores de propriedade em cinza claro não podem ser alterados com o uso deste aplicativo.  
  
## <a name="options"></a>Opções  
 **Caminho binário**  
 Exibe o local dos arquivos de programas usados por este serviço.  
  
 **Controle de erro**  
 1 indica "SERVICE_ERROR_NORMAL". Se o serviço não for iniciado durante a inicialização do computador, o programa de inicialização registrará o erro em log e exibirá uma caixa de mensagem pop-up, mas continuará a operação de inicialização. Esse valor não pode ser alterado.  
  
 **Código de saída**  
 Quando ocorre um erro, o número do erro é exibido nesta caixa. Use esse número para solucionar problemas de falhas procurando-o na Base de Dados de Conhecimento [!INCLUDE[msCoName](../../includes/msconame-md.md)] ou forneça o número à sua equipe de suporte técnico.  
  
 **Nome do host**  
 Exibe o nome do computador ou cluster que está executando a pesquisa de texto completo.  
  
 **Nome**  
 Indica o nome para exibição do serviço.  
  
 **ID do Processo**  
 Exibe a identificação do processo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 **Tipo de serviço do SQL**  
 Tipo de serviço fornecido a processos de chamada. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala vários serviços.  
  
 **Modo de início**  
 Defina este serviço com as seguintes opções:  
  
-   Manual: este serviço não é iniciado automaticamente na inicialização do computador. Você deve iniciá-lo usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager ou outra ferramenta.  
  
-   Automático: este serviço tenta ser iniciado na inicialização do computador.  
  
-   Desabilitado: este serviço não pode ser iniciado.  
  
 **Estado**  
 Indica se este serviço está sendo executado, se está parado ou desabilitado.  
  
## <a name="see-also"></a>Consulte Também  
 [Serviços do SQL Server](../../../2014/tools/configuration-manager/sql-server-services.md)  
  
  
