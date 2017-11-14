---
title: "Cenário RDS | Microsoft Docs"
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
ms.assetid: a7dcad87-aaf0-4b02-9660-472f8469761c
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 920df727d2714629a45280133c53011afccc5c4d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="rds-scenario"></a>Cenário RDS
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (veja o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/en-us/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Aplicativos que usam o RDS devem migrar para [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
 O aplicativo de catálogo de endereços é um cenário que mostra como usar Remote Data Service (RDS) para criar um aplicativo Web com reconhecimento de dados simple, um catálogo de endereços da empresa online. Este cenário é útil para Microsoft Visual Basic Scripting Edition (VBScript) e programadores COM que desejam saber como usar os controles ActiveX com reconhecimento de dados com o RDS e de software mais experiente desenvolvedores que desejam criar aplicativos Web centrados em dados.  
  
 Este cenário pressupõe que você saiba como usar marcas de layout HTML básico, técnicas de associação de dados use DHTML e programa com controles ActiveX.  
  
 Se você tiver instalado o SDK, o código-fonte completo para o aplicativo de exemplo do catálogo de endereços pode ser encontrado no diretório do SDK em samples\dataaccess\rds\AddressBook\AddressBook.asp. Para exibir o cenário de catálogo de endereços, digite no Internet Explorer 4.0 ou posterior,  **http://*webserver*/RDS/AddressBook/AddressBook.asp** onde *webserver* é o nome dada a seu computador Windows NT 4.0 ou Windows 2000 Web do servidor que está executando serviços de informações da Internet (IIS) e ASP.  
  
## <a name="introduction-to-address-book"></a>Introdução ao catálogo de endereços  
 O aplicativo de exemplo do catálogo de endereços fornece um catálogo de endereços online simples que você pode usar para publicar uma pasta de pesquisa em uma intranet. O catálogo de endereços foi projetado para que um usuário pode inserir uma cadeia de caracteres de pesquisa em um ou mais campos para solicitar informações sobre funcionários. Para mostrar os recursos básicos do serviço de dados remoto, o aplicativo de exemplo é intencionalmente mantido pequeno, com um número mínimo de objetos e campos de pesquisa.  
  
 A interface de aplicativo consiste das seguintes partes:  
  
-   Não visual **RDS. DataControl** objeto de associação de dados que é usado pelo cliente para se conectar ao banco de dados.  
  
-   Caixas de texto HTML que agem como campos de entrada para os critérios de pesquisa de atributos de funcionário.  
  
-   Botões de comando HTML para criar consultas, limpar os campos de pesquisa, atualizar o banco de dados com informações de funcionários, cancelar as alterações pendentes e navegue as linhas de dados exibidos na grade.  
  
-   DHTML associação de dados para exibir os dados retornados de consultas em um banco de dados de back-end (por meio de **RDS. DataControl** o objeto de associação de dados) em uma tabela.  
  
-   Rotinas de VBScript que se conectam a cada um dos elementos que foram mencionados anteriormente e permitir que eles interagem. Código VBScript também é usado para inicializar o **RDS. DataControl** de objeto e criar dinamicamente os cabeçalhos de coluna na tabela HTML dos nomes do **RDS. DataControl** campos de conjunto de registros.  
  
 Siga os links da etapa a etapa para configurar e executar o cenário de e para saber mais sobre como funciona o cenário.  
  
 Este cenário contém os tópicos a seguir.  
  
-   [Requisitos de sistema para o aplicativo de catálogo de endereços](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)  
  
-   [Executando o script SQL do catálogo de endereços](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)  
  
-   [Executando o aplicativo de exemplo do catálogo de endereços](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)  
  
-   [Objeto de associação de dados do catálogo de endereço](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)  
  
-   [Botões de comando do catálogo de endereços](../../../ado/guide/remote-data-service/address-book-command-buttons.md)  
  
-   [Botões de navegação do catálogo de endereços](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>Consulte também  
 [Requisitos de sistema para o aplicativo de catálogo de endereços](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)   
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)



