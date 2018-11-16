---
title: A propriedade de servidor (RDS) | Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- RDS::IBindMgr21::Server
helpviewer_keywords:
- Server property [RDS]
ms.assetid: d2727ce7-da9f-4271-ae3c-9334ef477c14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77ad00d9c21a7f7558f8f5cafc66464c1ffc54f7
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600176"
---
# <a name="server-property-rds"></a>Propriedade Server (RDS)
Indica o protocolo de comunicação e o nome de serviços de informações da Internet (IIS).  
  
 Você pode definir as **Server** propriedade em tempo de design nas marcas de objeto a[RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) de objeto ou no tempo de execução no código de script.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
 **HTTP**  
  
 Sintaxe de tempo de design  
  
```  
  
<PARAM NAME="Server" VALUE="http:  
//awebsrvr:port  
">  
  
```  
  
 Sintaxe de tempo de execução  
  
```  
  
DataControl  
.Server="https://  
awebsrvr:port  
"  
  
```  
  
 **HTTPS**  
  
 Sintaxe de tempo de design  
  
```  
  
<PARAM NAME="Server" VALUE="https://awebsrvr:port">  
```  
  
 Sintaxe de tempo de execução  
  
```  
  
DataControl.Server="https://awebsrvr:port"  
```  
  
 **DCOM**  
  
 Sintaxe de tempo de design  
  
```  
  
<PARAM NAME="Server" VALUE="  
computername  
">  
  
```  
  
 Sintaxe de tempo de execução  
  
```  
  
DataControl.Server="computername"  
```  
  
 **Em processo**  
  
 Sintaxe de tempo de design  
  
```  
  
<PARAM NAME="Server" VALUE="">  
  
```  
  
 Sintaxe de tempo de execução  
  
```  
  
DataControl.Server=""  
```  
  
## <a name="parameters"></a>Parâmetros  
 *awebsrvr*ou *computername*  
 Um **cadeia de caracteres** valor que contém uma Internet ou intranet caminho ou nome do computador, se o servidor estiver em um computador remoto; ou uma cadeia de caracteres vazia se o servidor estiver no computador local.  
  
 *port*  
 Opcional. Uma porta que é usada para se conectar a um servidor executando o IIS. O número da porta é definido no Internet Explorer (sobre o **exibição** menu, clique em **opções**e, em seguida, selecione o **Conexão** guia) ou no IIS.  
  
 *DataControl*  
 Uma variável de objeto que representa um **RDS. DataControl** objeto.  
  
## <a name="remarks"></a>Comentários  
 O servidor é o local onde o **RDS. DataControl** solicitação (ou seja, uma consulta ou atualização) é processada. Por padrão, todas as solicitações são processadas pelo [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto, [MSDFMAP. Manipulador](../../../ado/guide/remote-data-service/datafactory-customization.md) componente, e [MSDFMAP. INI](../../../ado/guide/remote-data-service/understanding-the-customization-file.md) arquivo no servidor especificado. Lembre-se de que ao alterar os servidores para reconciliar as configurações no antigo e novo **MSDFMAP. INI** arquivos. Incompatibilidades podem causar solicitações que ter êxito em um servidor falhar em outro. Se a propriedade do servidor é definida como a cadeia de caracteres vazia "", esses objetos serão usados no computador local.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade Server (VBScript)](../../../ado/reference/rds-api/server-property-example-vbscript.md)   
 [Propriedade Connect (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [Propriedade SQL](../../../ado/reference/rds-api/sql-property.md)   
 [Método SubmitChanges (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


