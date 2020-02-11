---
title: Classe SoapException do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- exceptions [Reporting Services], SoapException class
- SoapException class
ms.assetid: 2cec49ee-20b1-40eb-a75b-0908d9c05b34
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6f6efdfac89014116957990ef2db21cf52e76a4f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046022"
---
# <a name="reporting-services-soapexception-class"></a>Classe SoapException do Reporting Services
  Você deve tratar de erros específicos do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] que sabe que podem acontecer. Por exemplo, em um aplicativo onde você solicita que o usuário crie uma pasta, pode ser possível que ele tente criar uma pasta que já exista. Como desenvolvedor, você não tem controle sobre o que o usuário digita no nome da pasta e nos campos de caminho do seu aplicativo, mas tem controle sobre o que o usuário experimenta quando alguém incidentalmente tenta criar um item já existente.  
  
 Para facilitar a captura de condições de erro específicas, o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] classifica um código de erro para a exceção e retorna a classificação do erro usando propriedades da classe **SoapException**. Para obter mais informações, consulte "classe SoapException" na [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] documentação do SDK do.  
  
 A tabela a seguir lista as propriedades públicas da classe **SoapException**.  
  
|Propriedade pública|DESCRIÇÃO|  
|---------------------|-----------------|  
|**Ator**|O código que causou a exceção. O valor é a URL para o método do serviço Web.|  
|**Detalhes**|Informações de erro específicas do aplicativo. O valor é definido pelo servidor de relatório e está em formato XML. Para obter mais informações, consulte [Propriedade Detail](detail-property.md) e [Usando a propriedade Detail para tratar erros específicos](../best-practices/using-the-detail-property-to-handle-specific-errors.md).|  
|**HelpLink**|Uma URL ou URN para um arquivo de Ajuda associado ao erro. O valor é normalmente definido pelo serviço Web e define uma URL como Ajuda e Suporte do [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. Como o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] dá suporte a diversos links de ajuda para erros ocorridos, o servidor de relatório define informações de link de ajuda como parte da propriedade **Detail**. Para obter mais informações, consulte [Elemento HelpLink](helplink-element.md).|  
|**Mensagem**|Uma mensagem descritiva e localizada que descreve o erro. Esse texto poderia aparecer na interface do usuário do aplicativo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Introdução ao tratamento de exceção no Reporting Services](../introducing-exception-handling-in-reporting-services.md)   
 [Tabela de erros SoapException](soapexception-errors-table.md)  
  
  
