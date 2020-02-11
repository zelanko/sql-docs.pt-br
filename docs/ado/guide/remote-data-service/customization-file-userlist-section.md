---
title: Seção UserList do arquivo de personalização | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- UserList section in rds [ADO]
- customization file in RDS [ADO]
ms.assetid: 42e8ec20-eaac-4a95-8cb8-4bba93a75bcb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 558fd9c8379808e6c2f109a9c9584e8831cddd0f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922760"
---
# <a name="customization-file-userlist-section"></a>Seção UserList do arquivo de personalização
A seção **UserList** refere **-se** à seção Connect com o mesmo parâmetro de *identificador* de seção.  
  
 Esta seção pode conter uma *entrada de acesso de usuário*, que especifica direitos de acesso para o usuário especificado e substitui a *entrada de acesso* *padrão* na seção **conexão** correspondente.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Sintaxe  
 Uma entrada de acesso do usuário está no formato:  
  
 _nome de usuário_**=**   
 **_accessRights_**  
  
|Parte|DESCRIÇÃO|  
|----------|-----------------|  
|*Usu*|O *nome de usuário* da pessoa que emprega essa conexão. Nomes de usuário válidos são estabelecidos com a caixa de diálogo de **Service Manager** do IIS.|  
|**_accessRights_**|Um dos seguintes direitos de acesso:<br /><br /> -   **NoAccess** -o usuário não pode acessar a fonte de dados.<br />-   **ReadOnly** -o usuário pode ler a fonte de dados.<br />-   **ReadWrite** -o usuário pode ler ou gravar na fonte de dados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Seção conexão de arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [Seção de logs de arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [Seção SQL do arquivo de personalização](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [Personalização de datafactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Configurações do cliente necessárias](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Noções básicas sobre o arquivo de personalização](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Escrever seu próprio manipulador personalizado](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)


