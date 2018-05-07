---
title: Método ConvertToString (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ConvertToString method [ADO]
ms.assetid: b3f36bc8-6f69-49b0-83cd-2ccd3afebfbe
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da21cb2208e11ffa502b3788e36a1bc034ae1c33
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="converttostring-method-rds"></a>Método ConvertToString (RDS)
Converte um [registros](../../../ado/reference/ado-api/recordset-object-ado.md) em uma cadeia de caracteres MIME que representa os dados do conjunto de registros.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DataFactory.ConvertToString(Recordset)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *DataFactory*  
 Uma variável de objeto que representa um [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) objeto.  
  
 *Recordset*  
 Uma variável de objeto que representa um **registros** objeto.  
  
## <a name="remarks"></a>Remarks  
 Com arquivos. asp, use **ConvertToString** para inserir o **registros** em uma página HTML gerada no servidor para transportá-lo para um computador cliente.  
  
 **ConvertToString** carregado pela primeira vez o **registros** para o serviço de Cursor tabelas e, em seguida, gera um fluxo no formato MIME.  
  
 No cliente, o serviço de dados remoto pode converter a cadeia de caracteres MIME em um totalmente funcional **registros**. Ela funciona bem para tratamento de menos de 400 linhas de dados com não mais do que a largura de 1024 bytes por linha. Você não deve usá-lo para o fluxo de dados BLOB e grandes conjuntos de resultados por HTTP. Nenhuma compactação durante a transmissão é executada na cadeia de caracteres muito grandes conjuntos de dados levará um tempo considerável para transporte via HTTP quando comparado com o formato de otimização de transmissão tablegram definidos e implantados pelo serviço de dados remoto como seu formato de protocolo de transporte nativo.  
  
> [!NOTE]
>  Se você estiver usando o Active Server Pages para inserir a cadeia de caracteres MIME resultante em uma página HTML de cliente, lembre-se de que as versões anteriores à versão 2.0 do VBScript limitam tamanho da cadeia de caracteres para 32K. Se esse limite for excedido, um erro será retornado. Manter o escopo da consulta relativamente pequeno ao usar a inserção de MIME por meio de arquivos. ASP. Para corrigir isso, baixe a versão mais recente do VBScript do site Web de tecnologias de Script do Microsoft Windows.  
  
## <a name="applies-to"></a>Aplica-se a  
 [Objeto DataFactory (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo do método ConvertToString (VB)](../../../ado/reference/ado-api/converttostring-method-example-vb.md)   
 [Exemplo do método ConvertToString (VBScript)](../../../ado/reference/rds-api/converttostring-method-example-vbscript.md)


