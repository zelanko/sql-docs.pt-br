---
title: Cenário RDS | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: a7dcad87-aaf0-4b02-9660-472f8469761c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e936b6b68a67c1616a00d38f6d84776d44ef327
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/12/2018
ms.locfileid: "51559428"
---
# <a name="rds-scenario"></a>Cenário RDS
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 O aplicativo de catálogo de endereços é um cenário que mostra como usar o serviço de dados remota (RDS) para compilar um aplicativo Web simple e reconhecimento de dados — um catálogo de endereços da empresa online. Esse cenário é útil para Microsoft Visual Basic Scripting Edition (VBScript) e programadores de COM que desejam saber como usar controles ActiveX do reconhecimento de dados com o RDS e para o software experiente com mais desenvolvedores que desejam criar aplicativos Web centrados em dados.  
  
 Este cenário pressupõe que você sabe como usar marcas de layout HTML básica, técnicas de associação de dados do uso DHTML e programa com controles ActiveX.  
  
 Se você tiver instalado o SDK, o código-fonte completo para o aplicativo de exemplo do catálogo de endereços pode ser encontrado no diretório do SDK no samples\dataaccess\rds\AddressBook\AddressBook.asp. Para exibir o cenário de catálogo de endereços, no Internet Explorer 4.0 ou posterior, digite **https://*webserver*/RDS/AddressBook/AddressBook.asp** onde *webserver* é o nome dada a seu computador Windows NT 4.0 ou Windows 2000 Web do servidor que está executando serviços de informações da Internet (IIS) e o ASP.  
  
## <a name="introduction-to-address-book"></a>Introdução ao catálogo de endereços  
 O aplicativo de exemplo do catálogo de endereços fornece um catálogo de endereços de online simples que você pode usar para publicar um diretório pesquisável através de uma intranet. O catálogo de endereços foi projetado para que um usuário pode inserir uma cadeia de caracteres de pesquisa em um ou mais campos para solicitar informações sobre funcionários. Para mostrar os recursos básicos do serviço de dados remoto, o aplicativo de exemplo é intencionalmente mantido pequeno, com um número mínimo de objetos e campos de pesquisa.  
  
 A interface de aplicativo consiste das seguintes partes:  
  
-   Não visual **RDS. DataControl** objeto de associação de dados que é usado pelo cliente para se conectar ao banco de dados.  
  
-   Critérios de pesquisa de caixas de texto HTML que agem como campos de entrada para o atributo de funcionário.  
  
-   Botões de comando HTML para criar consultas, limpar os campos de pesquisa, atualizar o banco de dados com informações de funcionários, cancelar as alterações pendentes e navegar as linhas de dados exibidos na grade.  
  
-   Associação de dados do DHTML para exibir os dados retornados de consultas em relação a um banco de dados de back-end (por meio de **RDS. DataControl** o objeto de associação de dados) em uma tabela.  
  
-   Rotinas de VBScript que se conectam a cada um dos elementos que foram mencionados anteriormente e permitir que eles interajam. Código VBScript também é usado para inicializar o **RDS. DataControl** do objeto e criar dinamicamente os títulos de coluna na tabela HTML dos nomes do **RDS. DataControl** campos de conjunto de registros.  
  
 Siga os links da etapa para a etapa para configurar e executar o cenário de e para saber mais sobre como o cenário funciona.  
  
 Este cenário contém os tópicos a seguir.  
  
-   [Requisitos de sistema para o aplicativo de catálogo de endereços](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)  
  
-   [Executando o script SQL do catálogo de endereços](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)  
  
-   [Executando o aplicativo de exemplo do catálogo de endereços](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)  
  
-   [Objeto de associação de dados do catálogo de endereço](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)  
  
-   [Botões de comando do catálogo de endereços](../../../ado/guide/remote-data-service/address-book-command-buttons.md)  
  
-   [Botões de navegação do catálogo de endereços](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>Consulte também  
 [Requisitos do sistema para o aplicativo de catálogo de endereços](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)   
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)


