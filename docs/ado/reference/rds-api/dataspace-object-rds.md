---
title: "Objeto de espaço de dados (RDS) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- DataSpace object [RDS]
ms.assetid: 9194bffa-5bdf-4dff-af86-f7158c23bfa7
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3c4ee2e71334998cd0d2cba1c0c52c67e3314619
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="dataspace-object-rds"></a>Objeto de espaço de dados (RDS)
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Cria os proxies de cliente para objetos de negócios personalizada localizados na camada intermediária.  
  
 Serviço de dados remoto deve proxies do objeto comercial para que os componentes do lado do cliente podem se comunicar com os objetos comerciais localizados na camada intermediária. Proxies facilitam o empacotamento, a descompactação e do transporte (marshaling) do aplicativo [registros](../../../ado/reference/ado-api/recordset-object-ado.md) dados além dos limites do processos ou máquinas.  
  
 Serviço de dados remoto usa o **RDS. DataSpace** do objeto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método para criar os proxies do objeto de negócios. O proxy do objeto business é criado dinamicamente sempre que uma instância de sua contraparte do objeto comercial de camada intermediária é criada. Serviço de dados remoto suporta os seguintes protocolos: HTTP, HTTPS (HTTP Secure Sockets), DCOM e em processo (componentes cliente e o objeto comercial que residem no mesmo computador).  
  
> [!NOTE]
>  RDS se comporta de maneira "sem monitoração de estado" quando o **RDS. DataSpace** objeto usa os protocolos HTTP ou HTTPS. Ou seja, todas as informações internas sobre uma solicitação de cliente serão descartadas após o servidor retorna uma resposta.  
  
> [!NOTE]
>  Embora o objeto comercial parece existe para o tempo de vida do proxy do objeto comercial, o objeto comercial realmente existe até que uma resposta será enviada a uma solicitação. Quando uma solicitação é emitida (ou seja, um método é chamado no objeto comercial), o proxy abre uma nova conexão para o servidor e o servidor cria uma nova instância do objeto comercial. Depois que o objeto comercial responde à solicitação, o servidor destrói o objeto comercial e fecha a conexão.  
  
> [!NOTE]
>  Esse comportamento significa que você não pode passar dados de uma solicitação para outro usando uma propriedade de objeto de negócios ou variável. Você deve aplicar outro mecanismo, como um arquivo ou um argumento de método para manter dados de estado.  
  
 A ID de classe para o **RDS. DataSpace** objeto é 0-983A-00C04FC29E36 BD96C556 65A3 - 11 D.  
  
 O **DataSpace** objeto é seguro para script.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método CreateObject e objeto DataSpace (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)


