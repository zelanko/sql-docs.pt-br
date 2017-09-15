---
title: Propriedade de manipulador (RDS) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Handler property [ADO]
ms.assetid: fdc34362-6d47-4727-b171-8d033159408e
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 25ac7c676fbab1e8b5899a3502fab2199b0afd22
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="handler-property-rds"></a>Propriedade de manipulador (RDS)
Indica o nome de um programa de personalização do lado do servidor (manipulador) que estende a funcionalidade do [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)e os parâmetros usados pelo *manipulador*.  
  
 **Aplica-se a:** [DataControl objeto (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataControl.Handler = String  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataControl*  
 Uma variável de objeto que representa um [RDS. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) objeto.  
  
 *Cadeia de caracteres*  
 Um **cadeia de caracteres** valor que contém o nome do manipulador e os parâmetros, todos separados por vírgulas (por exemplo, `"handlerName,parm1,parm2,...,parm` *N*`"`).  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade oferece suporte a [personalização](../../../ado/guide/remote-data-service/datafactory-customization.md), uma funcionalidade que exija configuração o [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propriedade **adUseClient**.  
  
 O nome do manipulador e seus parâmetros, se houver, são separados por vírgulas (","). Um comportamento imprevisível ocorrerá se um ponto e vírgula (";") é exibido em qualquer lugar na *cadeia de caracteres*. Você pode escrever seu próprio manipulador, desde que ele oferece suporte a **IDataFactoryHandler** interface.  
  
 O nome do manipulador padrão é **MSDFMAP. Manipulador**, e seu parâmetro padrão é um arquivo de personalização chamado **MSDFMAP. INI**. Use essa propriedade para invocar os arquivos de personalização alternativo criados pelo administrador do servidor.  
  
 A alternativa à configuração o **manipulador** é de propriedade para especificar um manipulador e parâmetros no [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propriedade; ou seja, "**manipulador =** * handlerName, parameter1, parameter2,...; *".  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo da propriedade manipulador (VB)](../../../ado/reference/rds-api/handler-property-example-vb.md)   
 [Personalização do DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)



