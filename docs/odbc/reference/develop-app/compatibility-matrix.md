---
title: Matriz de compatibilidade | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application compatibility issues [ODBC]
- application upgrades [ODBC], compatibility matrix
- upgrading applications [ODBC], compatibility matrix
ms.assetid: 0690b463-15a1-48fa-9d0b-9cc9e5bf7fc6
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6c3a7fac17ed685680e71b329388e192ec1c9f97
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="compatibility-matrix"></a>Matriz de compatibilidade
A tabela a seguir descreve a compatibilidade dos tipos de aplicativos e drivers definidas anteriormente nesta seção.  
  
|Tipo de aplicativo<br /><br /> e versão|ODBC de 32 bits<br /><br /> 2.*x* driver|ODBC 3. *x*<br /><br /> Driver|Driver ODBC 3.8|ISO e abrir grupo compatível com o driver|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|aplicativos de 16 bits, qualquer versão|Compatível|Compatível|Compatível|Compatível|  
|2 puro. *x* aplicativo|Compatível|Compatível|Compatível|Não compatível com [3]|  
|2 puro. *x* recompilado aplicativo|Compatível|Compatível com a [1]|Compatível com a [1]|Não compatível com [3]|  
|2 puro. *x* aplicativo Unicode|Compatível|Compatível com a [1]|Compatível com a [1]|Não compatível com [3]|  
|Aplicativo puro Open Group e compatível com ISO|Não é compatível|Compatível com o [2]|Compatível com o [2]|Compatível com o [2]|  
|Aplicativo 3.0 puro|Não é compatível|Compatível|Compatível|Não compatível com [4]|  
|Aplicativo 3.5 puro|Não é compatível|Compatível|Compatível|Não compatível com [4]|  
|Aplicativo puro 3.8 (ou superior)|Não compatível com [5]|Não compatível com [5]|Compatível|Não compatível com [4]|  
|Aplicativo substituído|Compatível|Compatível|Compatível|Não compatível com [3]|  
  
 [1], o aplicativo deve recompilar usando cabeçalhos ODBC 3.5 (ou superior) com a opção UNICODE (se for um aplicativo Unicode) e configure ODBCVER para 0x0250.  
  
 [2], o aplicativo deve compilar usando cabeçalhos ODBC 3.5 (ou superior) e vincule com o Gerenciador de Driver ODBC. Ele também deve definir o sinalizador de cabeçalho ODBC_STD.  
  
 [3] essa configuração potencialmente pode não funcionar porque não há recursos no ODBC 2. *x* que não estão em padrões, como indicadores.  
  
 [4] esta configuração pode potencialmente não funcionará porque não há recursos no ODBC 3*. x* que não estão em padrões, como indicadores.  
  
 [5] esta configuração pode potencialmente falhar porque não há recursos que não estão no ODBC 2. x ou 3. x drivers, como específicos do driver no ODBC 3.8 [tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
## <a name="driver-manager-compatibility"></a>Compatibilidade do Gerenciador de driver  
 Um aplicativo ODBC 3.0 que deve funcionar com todas as versões do Gerenciador de Driver deve fazer o seguinte na inicialização:  
  
-   Alocar um identificador de ambiente.  
  
-   Defina o atributo do ambiente de SQL_ATTR_ODBC_VERSION para SQL_OV_ODBC3_80. Se o Gerenciador de Driver retornará SQL_ERROR, o Gerenciador de Driver é anterior 3.8. Redefina SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3 ou SQL_OV_ODBC2, conforme apropriado, para corresponder ao Gerenciador de Driver.  
  
-   Alocar um identificador de conexão.  
  
-   Fazer uma conexão.  
  
-   Chame SQLGetInfo para SQL_DRIVER_ODBC_VER determinar a versão do driver. Se o driver é um driver de ODBC 3.8, você pode usar tipos de C específicos do driver. Caso contrário, não use tipos de dados C específicos do driver.  
  
 Observe que um aplicativo de 3. x recompilado ODBC pode usar os recursos de ODBC 3.8 diferentes tipos de C específicos do driver sem especificar SQL_OV_ODBC3_80 para SQL_ATTR_ODBC_VERSION. Isso é semelhante a um aplicativo de 2. x ODBC recompilado usando recursos do ODBC 3. x.  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>Usando SQLCancelHandle em um aplicativo compatível com todos os gerenciadores de Driver  
 Porque [SQLCancelHandle função](../../../odbc/reference/syntax/sqlcancelhandle-function.md) não tem suporte em gerenciadores de Driver que foram lançadas antes do Windows 7, um aplicativo não pode ser carregado em versões mais antigas do Windows se chama **SQLCancelHandle** diretamente. Para trabalhar com todas as versões do Driver de gerentes e usar **SQLCancelHandle** em novas versões do Windows, um aplicativo deve chamar **SQLCancelHandle** indiretamente usando **LoadLibrary** e **GetProcAddress.**  
  
## <a name="see-also"></a>Consulte Também  
 [Novidades no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
