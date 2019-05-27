---
title: Controlar a distribuição de relatórios | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], report distribution
- subscriptions [Reporting Services], e-mail
- subscriptions [Reporting Services], file share delivery
- file share delivery [Reporting Services]
- e-mail [Reporting Services]
- subscriptions [Reporting Services], security
- mail [Reporting Services]
ms.assetid: 8f15e2c6-a647-4b05-a519-1743b5d8654c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: de8a27801ef89f10bf303cee17d1c2d0e1081c5a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66109695"
---
# <a name="control-report-distribution"></a>Controlar a distribuição de relatórios
  Você pode configurar um servidor de relatório para reduzir os riscos de segurança associados à distribuição de emails e de compartilhamentos de arquivos.  
  
## <a name="securing-reports"></a>Protegendo relatórios  
 A primeira etapa para controlar a distribuição de relatório é proteger o relatório contra o acesso não autorizado. Para ser usado em uma assinatura, o relatório deve usar um conjunto armazenado de credenciais que não variam para entregas individuais. Qualquer usuário que pode acessar o relatório no servidor de relatório pode executá-lo e possivelmente distribuí-lo. Para impedir que isto aconteça, você deve limitar o acesso somente aos usuários que precisam do relatório. Para obter mais informações, consulte [proteger relatórios e recursos](security/secure-reports-and-resources.md) e [proteger pastas](security/secure-folders.md).  
  
 Relatórios extremamente confidenciais que usam a segurança de banco de dados para autorizar o acesso não podem ser distribuídos por meio de assinaturas.  
  
> [!IMPORTANT]  
>  Os relatórios são transportados como arquivos. Os riscos e as proteções que se aplicam aos arquivos também se aplicam aos relatórios salvos em disco ou enviados como anexos. Qualquer usuário que tem acesso a um arquivo pode distribuir ou usar o arquivo como desejar.  
  
## <a name="controlling-e-mail-delivery"></a>Controlando a entrega de emails  
 Você pode configurar um servidor de relatório para limitar a distribuição de emails a domínios host específicos. Por exemplo, é possível impedir que um servidor de relatório entregue um relatório para todos os domínios, com exceção dos listados no arquivo de configuração RSReportServer.  
  
 Você também pode definir configurações para ocultar o campo **Para** em uma assinatura. Neste caso, os relatórios são entregues somente ao usuário que define a assinatura. No entanto, depois que um relatório é enviado a um usuário, você não pode impedir explicitamente seu encaminhamento.  
  
 A maneira mais eficaz de controlar a distribuição de relatórios é configurar um servidor de relatório para enviar somente uma URL de servidor de relatório. O servidor de relatório usa a Autenticação do Windows e um modelo de autorização baseado em funções para controlar o acesso a um relatório. Se o usuário receber automaticamente por email um relatório que não tem autorização para exibir, o servidor de relatório não exibirá o relatório.  
  
## <a name="controlling-file-share-delivery"></a>Controlando a entrega de compartilhamentos de arquivos  
 A entrega de compartilhamentos de arquivos é usada para enviar um relatório a um arquivo em um disco rígido. Depois de ser salvo em disco, o arquivo não pode mais ser submetido ao modelo de segurança baseado em funções que o servidor de relatório usa para controlar o acesso do usuário. Para proteger um relatório que foi entregue em disco, coloque listas de controle de acesso (ACLs) no próprio arquivo ou na pasta que o contém. Opções de segurança adicionais podem estar disponíveis, dependendo do sistema operacional.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar um servidor de relatório para entrega de email &#40;Configuration Manager do SSRS&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [Assinaturas e entrega &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Criar e gerenciar assinaturas de servidores de relatório no modo Nativo](../../2014/reporting-services/create-manage-subscriptions-native-mode-report-servers.md)  
  
  
