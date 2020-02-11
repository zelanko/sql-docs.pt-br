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
ms.openlocfilehash: 665afeb4be263ae0772557d2d2f30e112596f289
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922443"
---
# <a name="rds-scenario"></a>Cenário RDS
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 O aplicativo de catálogo de endereços é um cenário que mostra como usar o RDS (serviço de dados remotos) para criar um aplicativo Web simples e com reconhecimento de dados – um catálogo de endereços corporativos online. Esse cenário é útil para Microsoft Visual Basic Scripting Edition (VBScript) e programadores COM que desejam aprender a usar controles ActiveX com reconhecimento de dados com o RDS e para desenvolvedores de software mais experientes que desejam criar aplicativos Web centrados em dados.  
  
 Esse cenário pressupõe que você saiba como usar marcas básicas de layout HTML, usar técnicas de ligação de dados DHTML e programar com controles ActiveX.  
  
 Se você instalou o SDK, o código-fonte completo do aplicativo de exemplo do catálogo de endereços pode ser encontrado no diretório do SDK em samples\dataaccess\rds\AddressBook\AddressBook.asp. Para exibir o cenário do catálogo de endereços, no Internet Explorer 4,0 ou posterior, digite **https://*WebServer*/RDS/AddressBook/AddressBook.asp** , em que *WebServer* é o nome fornecido para o computador do servidor Web Windows NT 4,0 ou Windows 2000 que está executando serviços de informações da Internet (IIS) e ASP.  
  
## <a name="introduction-to-address-book"></a>Introdução ao catálogo de endereços  
 O aplicativo de exemplo do catálogo de endereços fornece um simples catálogo de endereços online que você pode usar para publicar um diretório pesquisável em uma intranet. O catálogo de endereços foi projetado para que um usuário possa inserir uma cadeia de caracteres de pesquisa em um ou mais campos para solicitar informações sobre os funcionários. Para mostrar os recursos básicos do Remote Data Service, o aplicativo de exemplo é mantido intencionalmente pequeno, com um número mínimo de objetos e campos de pesquisa.  
  
 A interface do aplicativo consiste nas seguintes partes:  
  
-   Um RDS não Visual **. **Objeto de associação de dados de DataControl que é usado pelo cliente para se conectar ao Database.  
  
-   Caixas de texto HTML que atuam como campos de entrada para critérios de pesquisa de atributo de funcionário.  
  
-   Botões de comando HTML para criar consultas, limpar campos de pesquisa, atualizar o banco de dados com informações de funcionários, cancelar alterações pendentes e navegar pelas linhas de dado exibidas na grade.  
  
-   Ligação de dados DHTML para exibir dados retornados de consultas em um banco de dados back-end (por meio do **RDS. **Objeto de vinculação de dados de DataControl) em uma tabela.  
  
-   Rotinas do VBScript que conectam cada um dos elementos que foram mencionados anteriormente e permitem que eles interajam. O código VBScript também é usado para inicializar o **RDS. Objeto DataControl** e cria dinamicamente os cabeçalhos de coluna na tabela HTML com os nomes de **RDS. **Campos do conjunto de registros de DataControl.  
  
 Siga os links da etapa para a etapa para configurar e executar o cenário e para saber mais sobre como o cenário funciona.  
  
 Esse cenário contém os tópicos a seguir.  
  
-   [Requisitos de sistema para o aplicativo de catálogo de endereços](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)  
  
-   [Executar o script SQL do catálogo de endereços](../../../ado/guide/remote-data-service/running-the-address-book-sql-script.md)  
  
-   [Executar o aplicativo de exemplo do catálogo de endereços](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)  
  
-   [Objeto de associação de dados do catálogo de endereço](../../../ado/guide/remote-data-service/address-book-data-binding-object.md)  
  
-   [Botões de comando do catálogo de endereços](../../../ado/guide/remote-data-service/address-book-command-buttons.md)  
  
-   [Botões de navegação do catálogo de endereços](../../../ado/guide/remote-data-service/address-book-navigation-buttons.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Requisitos do sistema para o aplicativo de catálogo de endereços](../../../ado/guide/remote-data-service/system-requirements-for-the-address-book-application.md)   
 [Microsoft ActiveX Data Objects (ADO)](../../../ado/microsoft-activex-data-objects-ado.md)   
 [Conceitos básicos do RDS](../../../ado/guide/remote-data-service/rds-fundamentals.md)   
 [Tutorial RDS](../../../ado/guide/remote-data-service/rds-tutorial.md)


