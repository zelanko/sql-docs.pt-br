---
title: Seção UserList do arquivo de personalização | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- UserList section in rds [ADO]
- customization file in RDS [ADO]
ms.assetid: 42e8ec20-eaac-4a95-8cb8-4bba93a75bcb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 70d22fd83574d2d99724fb507c8b0916b07d7373
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47667584"
---
# <a name="customization-file-userlist-section"></a>Seção UserList do arquivo de personalização
O **userlist** seção se refere à **connect** seção com a mesma seção *identificador* parâmetro.  
  
 Esta seção pode conter um *entrada de acesso de usuário*, que especifica o acesso de direitos para o usuário especificado e substitui o *padrão* *acessar entrada* na correspondência de **conectar** seção.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
 Uma entrada de acesso do usuário está no formato:  
  
 *userName* **=**   
 ***accessRights***  
  
|Parte|Description|  
|----------|-----------------|  
|*userName*|O *nome de usuário* da pessoa empregando essa conexão. Nomes de usuário válidos são estabelecidos com o IIS **do Service Manager** caixa de diálogo.|  
|***accessRights***|Um dos seguintes direitos de acesso:<br /><br /> -   **NoAccess** — usuário não pode acessar a fonte de dados.<br />-   **ReadOnly** — o usuário pode ler a fonte de dados.<br />-   **ReadWrite** — usuário pode ler ou gravar na fonte de dados.|  
  
## <a name="see-also"></a>Consulte também  
 [Seção conexão do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Seção de Logs do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Seção SQL do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Personalização do DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configurações de cliente necessárias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Noções básicas sobre o arquivo de personalização](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escrevendo seu próprio manipulador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


