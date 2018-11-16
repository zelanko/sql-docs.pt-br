---
title: Objeto DataSpace (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- DataSpace object [RDS]
ms.assetid: 9194bffa-5bdf-4dff-af86-f7158c23bfa7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d75a5dcd8a09388c031e4e01c8bb8b9c1d62bb80
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600556"
---
# <a name="dataspace-object-rds"></a>Objeto DataSpace (RDS)
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Cria os proxies do lado do cliente a objetos comerciais personalizados localizados na camada intermediária.  
  
 Serviço de dados remoto precisa proxies de objeto de negócios para que os componentes do lado do cliente podem se comunicar com os objetos de negócios localizados na camada intermediária. Proxies de facilitam o empacotamento, a descompactação e do transporte (marshaling) do aplicativo [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) dados entre os limites de processo ou computadores.  
  
 Serviço de dados remoto usa o **RDS. DataSpace** do objeto [CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md) método para criar proxies do objeto de negócios. O proxy do objeto de negócios é criado dinamicamente sempre que uma instância de sua contraparte do objeto de negócios de camada intermediária é criada. Serviço de dados remoto oferece suporte a protocolos a seguir: HTTP, HTTPS (HTTP Secure Sockets), DCOM e em processo (componentes do cliente e o objeto de negócios que residem no mesmo computador).  
  
> [!NOTE]
>  RDS se comporta de maneira "sem monitoração de estado" quando o **RDS. DataSpace** objeto usa os protocolos HTTP ou HTTPS. Ou seja, todas as informações internas sobre uma solicitação do cliente serão descartadas após o servidor retorna uma resposta.  
  
> [!NOTE]
>  Embora o objeto comercial pareça existir para o tempo de vida do proxy do objeto comercial, o objeto comercial realmente existe até que uma resposta é enviada a uma solicitação. Quando uma solicitação é emitida (ou seja, um método é chamado no objeto de negócios), o proxy abre uma nova conexão para o servidor e o servidor cria uma nova instância do objeto comercial. Depois que o objeto comercial responde à solicitação, o servidor destrói o objeto comercial e fecha a conexão.  
  
> [!NOTE]
>  Esse comportamento significa que você não pode passar dados de uma solicitação para outra usando uma propriedade de objeto de negócios ou variável. Você deve empregar algum outro mecanismo, como um arquivo ou um argumento de método, para manter os dados de estado.  
  
 A ID de classe para o **RDS. DataSpace** objeto é BD96C556-65A3 - 11 D 0 983A 00C04FC29E36.  
  
 O **DataSpace** objeto é seguro para script.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos do objeto DataSpace (RDS)](../../../ado/reference/rds-api/dataspace-object-rds-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método CreateObject e objeto DataSpace (VBScript)](../../../ado/reference/rds-api/dataspace-object-and-createobject-method-example-vbscript.md)


