---
description: Matriz de compatibilidade
title: Matriz de compatibilidade | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application compatibility issues [ODBC]
- application upgrades [ODBC], compatibility matrix
- upgrading applications [ODBC], compatibility matrix
ms.assetid: 0690b463-15a1-48fa-9d0b-9cc9e5bf7fc6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bafe3d85e1f4dc1c18acb057fe8c00e4ca0b36d0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461558"
---
# <a name="compatibility-matrix"></a>Matriz de compatibilidade
A tabela a seguir descreve a compatibilidade dos tipos de aplicativos e drivers definidos anteriormente nesta seção.  
  
|Tipo de aplicativo<br /><br /> e versão|ODBC de 32 bits<br /><br /> Driver *2. x*|ODBC *3. x*<br /><br /> Driver|Driver ODBC 3,8|ISO e abrir o driver em conformidade com o grupo|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|aplicativo de 16 bits, qualquer versão|Compatível|Compatível|Compatível|Compatível|  
|Aplicativo puro *2. x*|Compatível|Compatível|Compatível|Não compatível [3]|  
|Aplicativo recompilado de *2. x* puro|Compatível|Compatível [1]|Compatível [1]|Não compatível [3]|  
|Aplicativo Unicode puro *2. x*|Compatível|Compatível [1]|Compatível [1]|Não compatível [3]|  
|Aplicativo puro de Open Group e ISO-compliant|Não compatível|Compatível [2]|Compatível [2]|Compatível [2]|  
|Aplicativo puro 3,0|Não compatível|Compatível|Compatível|Não compatível [4]|  
|Aplicativo puro 3,5|Não compatível|Compatível|Compatível|Não compatível [4]|  
|Aplicativo puro 3,8 (ou superior)|Não compatível [5]|Não compatível [5]|Compatível|Não compatível [4]|  
|Aplicativo substituído|Compatível|Compatível|Compatível|Não compatível [3]|  
  
 [1] o aplicativo deve recompilar usando cabeçalhos ODBC 3,5 (ou superior) com a opção UNICODE (se for um aplicativo Unicode) e deve definir ODBCVER como 0x0250.  
  
 [2] o aplicativo deve compilar usando os cabeçalhos ODBC 3,5 (ou superior) e vincular com o Gerenciador de driver ODBC. Ele também deve definir o sinalizador de cabeçalho ODBC_STD.  
  
 [3] essa configuração pode potencialmente falhar ao funcionar porque há recursos no ODBC *2. x* que não estão nos padrões, como indicadores.  
  
 [4] essa configuração pode potencialmente falhar ao funcionar porque há recursos no ODBC *3. x* que não estão nos padrões, como indicadores.  
  
 [5] essa configuração pode potencialmente falhar porque há recursos no ODBC 3,8 que não estão em drivers ODBC 2. x ou 3. x, como [tipos de dados C específicos do driver no ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
## <a name="driver-manager-compatibility"></a>Compatibilidade do Gerenciador de driver  
 Um aplicativo ODBC 3,0 que deve operar com todas as versões do Gerenciador de driver deve fazer o seguinte na inicialização:  
  
-   Aloque um identificador de ambiente.  
  
-   Defina o atributo de ambiente SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3_80. Se o Gerenciador de driver retornar SQL_ERROR, o Gerenciador de driver será mais antigo que 3,8. Redefina SQL_ATTR_ODBC_VERSION para SQL_OV_ODBC3 ou SQL_OV_ODBC2, conforme apropriado, para corresponder ao Gerenciador de driver.  
  
-   Aloque um identificador de conexão.  
  
-   Faça uma conexão.  
  
-   Chame SQLGetInfo para SQL_DRIVER_ODBC_VER para determinar a versão do driver. Se o driver for um driver ODBC 3,8, você poderá usar tipos C específicos do driver. Caso contrário, não use tipos de dados C específicos do driver.  
  
 Observe que um aplicativo ODBC 3. x recompilado pode usar recursos ODBC 3,8 diferentes de tipos C específicos do driver sem especificar SQL_OV_ODBC3_80 para SQL_ATTR_ODBC_VERSION. Isso é semelhante a um aplicativo ODBC 2. x recompilado usando os recursos do ODBC 3. x.  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>Usando SQLCancelHandle em um aplicativo compatível com todos os gerenciadores de driver  
 Como a [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) não tem suporte em gerenciadores de driver que foram lançados antes do Windows 7, um aplicativo não poderá ser carregado em versões anteriores do Windows se ele chamar **SQLCancelHandle** diretamente. Para trabalhar com todas as versões dos gerenciadores de drivers e usar o **SQLCancelHandle** em novas versões do Windows, um aplicativo deve chamar **SQLCancelHandle** indiretamente usando **LoadLibrary** e **GetProcAddress.**  
  
## <a name="see-also"></a>Consulte Também  
 [Novidades no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
