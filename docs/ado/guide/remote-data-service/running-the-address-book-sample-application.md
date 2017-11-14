---
title: "Executando o aplicativo de exemplo do catálogo de endereço | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 3a2644e9-d634-4ae6-a5b7-13fb7b317ec7
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: dca092267dfba700e1d079f8d2147c7f204e6e32
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="running-the-address-book-sample-application"></a>Executando o aplicativo de exemplo do catálogo de endereços
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Para executar o aplicativo de catálogo de endereços, siga este procedimento.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
### <a name="to-run-this-application"></a>Para executar este aplicativo  
  
1.  Certifique-se de que o Microsoft SQL Server está em execução. Clique em **iniciar**, aponte para **programas**, aponte para **Microsoft SQL Server 7.0**e, em seguida, clique em **do Service Manager**. Se houver uma seta verde no círculo branco, em seguida, do SQL Server está em execução. Se não for (haverá um quadrado vermelho no círculo branco), clique em **iniciar/continuar**.  
  
2.  No Microsoft Internet Explorer 4.0 ou posterior, digite o seguinte endereço:  
  
     **http://** *webserver* **/RDS/AddressBook/AddrBook.asp**  
  
     onde *webserver* é o nome do servidor Web onde os componentes de servidor RDS estão instalados.  
  
3.  Em seguida, você pode tentar vários cenários em que o aplicativo de exemplo do catálogo de endereços, como procurar por uma pessoa com base no seu nome de email, listando todas as pessoas com o título "Gerente de programas", ou existente de edição de registros. Clique em **localizar** para preencher a grade de dados com todos os nomes disponíveis.  
  
## <a name="see-also"></a>Consulte também  
 [Objeto de associação de dados do catálogo de endereço](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)





