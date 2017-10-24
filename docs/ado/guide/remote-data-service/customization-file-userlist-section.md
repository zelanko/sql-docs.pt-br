---
title: "Personalização do arquivo UserList seção | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- UserList section in rds [ADO]
- customization file in RDS [ADO]
ms.assetid: 42e8ec20-eaac-4a95-8cb8-4bba93a75bcb
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5521648ed1c4d125168d3f9afb7a4c884854d9b4
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="customization-file-userlist-section"></a>Seção do arquivo UserList de personalização
O **userlist** seção se refere ao **conectar** seção com a mesma seção *identificador* parâmetro.  
  
 Esta seção pode conter um *entrada de acesso do usuário*, que especifica o acesso de direitos para o usuário especificado e substitui o *padrão* *acessar entrada* na correspondência de **conectar** seção.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
 É uma entrada de acesso do usuário do formulário:  
  
 *nome de usuário***=**   
 ***accessRights***  
  
|Parte|Description|  
|----------|-----------------|  
|*nome de usuário*|O *nome de usuário* da pessoa que utilize essa conexão. Nomes de usuário válidos são estabelecidos com o IIS **do Service Manager** caixa de diálogo.|  
|***accessRights***|Um dos seguintes direitos de acesso:<br /><br /> -   **NoAccess** — usuário não pode acessar a fonte de dados.<br />-   **ReadOnly** — o usuário pode ler a fonte de dados.<br />-   **ReadWrite** — usuário pode ler ou gravar para a fonte de dados.|  
  
## <a name="see-also"></a>Consulte também  
 [Arquivo de personalização de conectar-se a seção](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Seção de Logs do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Seção SQL do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Personalização do DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configurações de cliente necessárias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Noções básicas sobre o arquivo de personalização](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escrevendo seu próprio manipulador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



