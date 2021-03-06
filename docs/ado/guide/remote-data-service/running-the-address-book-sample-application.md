---
description: Executar o aplicativo de exemplo do catálogo de endereços
title: Executando o aplicativo de exemplo do catálogo de endereços | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 3a2644e9-d634-4ae6-a5b7-13fb7b317ec7
author: rothja
ms.author: jroth
ms.openlocfilehash: 85d9dbf43107af7504241af825b5b21c38139e3b
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91723049"
---
# <a name="running-the-address-book-sample-application"></a>Executar o aplicativo de exemplo do catálogo de endereços
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
 Para executar o aplicativo de catálogo de endereços, siga este procedimento.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
### <a name="to-run-this-application"></a>Para executar este aplicativo  
  
1.  Verifique se Microsoft SQL Server está em execução. Clique em **Iniciar**, aponte para **programas**, aponte para **Microsoft SQL Server 7,0**e clique em **Service Manager**. Se houver uma seta verde no círculo branco, SQL Server estará em execução. Se não for (haverá um quadrado vermelho no círculo branco), clique em **Iniciar/continuar**.  
  
2.  No Microsoft Internet Explorer 4,0 ou posterior, digite o seguinte endereço:  
  
     **/RDS/AddressBook/AddrBook.asp** **https://** *WebServer*  
  
     em que *WebServer* é o nome do servidor Web onde os componentes do servidor RDS estão instalados.  
  
3.  Em seguida, você pode experimentar vários cenários no aplicativo de exemplo do catálogo de endereços, como Pesquisar por uma pessoa com base em seu nome de email, listando todas as pessoas com o título "gerente de programas" ou editando registros existentes. Clique em **Localizar** para preencher a grade de dados com todos os nomes disponíveis.  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto de associação de dados do catálogo de endereço](./address-book-data-binding-object.md)