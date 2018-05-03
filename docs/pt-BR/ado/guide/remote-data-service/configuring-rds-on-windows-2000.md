---
title: Configurando o RDS no Windows 2000 | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS configuration [ADO], Windows 2000
ms.assetid: ef37e858-c05f-4f52-a65f-3ce6037e0d03
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c1a85b322b48a19bd8b8d7bbf8777fe03c780371
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="configuring-rds-on-windows-2000"></a>Configurando o RDS no Windows 2000
Se você tiver dificuldade obtendo RDS funcione corretamente após a atualização para o Windows 2000, siga estas etapas para solucionar o problema:  
  
1.  Certifique-se de que o serviço de publicação na World Wide Web está em execução primeiro, navegando até http:// servidor usando o Internet Explorer. Se você não pode acessar o servidor Web dessa maneira, abra um prompt de comando e digite o comando a seguir, "NET iniciar W3SVC".  
  
2.  No menu Iniciar, selecione Executar. Digite msdfmap.ini e, em seguida, clique em Okey para abrir o arquivo msdfmap.ini no bloco de notas. Verifique a seção [conectar padrão] e se o parâmetro de acesso é definido como NOACCESS, altere-a como somente leitura.  
  
3.  Usando o utilitário RegEdit, navegue para "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\DataFactory\HandlerInfo" e certifique-se de **HandlerRequired** é definido como 0 e **DefaultHandler** é "" (nulo a cadeia de caracteres).  
  
     **Observação** se você fizer alterações a esta seção do registro, você deve parar e reiniciar o serviço de publicação na World Wide Web digitando os seguintes comandos no prompt de comando: "NET STOP W3SVC" e "NET iniciar W3SVC".  
  
4.  Usando o utilitário RegEdit, navegue no registro para "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W3SVC\Parameters\ADCLaunch" e verifique se há uma chave chamada **RDSServer.Datafactory**. Caso contrário, crie-o.  
  
5.  Usando o Gerenciador de serviços de Internet, localize o site da Web padrão e exibir as propriedades da raiz virtual MSADC. Inspecione a pasta segurança/endereço IP e restrições de nome de domínio. Se o "acesso negado" estiver marcado, selecione "Concedido".  
  
 Certifique-se de tentar reinicializar o servidor se as alterações não aparecem resolver o problema primeiro.  
  
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565). Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows. Migrar aplicativos que usam o RDS para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="see-also"></a>Consulte também  
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)


