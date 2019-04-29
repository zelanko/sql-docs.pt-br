---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1d0fc510c7c45dab8fbc79cc8e74001ff1855b6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63026573"
---
# <a name="compatibility-matrix"></a>Matriz de compatibilidade
A tabela a seguir descreve a compatibilidade dos tipos de aplicativos e drivers definidos anteriormente nesta seção.  
  
|Tipo de aplicativo<br /><br /> e versão|ODBC de 32 bits<br /><br /> 2.*x* driver|ODBC 3.*x*<br /><br /> Driver|Driver ODBC 3.8|ISO e abra grupo compatível com o driver|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|aplicativo de 16 bits, qualquer versão|Compatível|Compatível|Compatível|Compatível|  
|2 puro. *x* aplicativo|Compatível|Compatível|Compatível|Não compatível com [3]|  
|2 puro. *x* recompilado aplicativo|Compatível|Compatível com [1]|Compatível com [1]|Não compatível com [3]|  
|2 puro. *x* aplicativo Unicode|Compatível|Compatível com [1]|Compatível com [1]|Não compatível com [3]|  
|Aplicativo puro Open Group e compatível com ISO|Não é compatível|Compatível com [2]|Compatível com [2]|Compatível com [2]|  
|Aplicativo 3.0 puro|Não é compatível|Compatível|Compatível|Não compatível com [4]|  
|Aplicativo de 3,5 puro|Não é compatível|Compatível|Compatível|Não compatível com [4]|  
|Aplicativo puro de 3,8 (ou superior)|Não compatível com [5]|Não compatível com [5]|Compatível|Não compatível com [4]|  
|Aplicativo substituído|Compatível|Compatível|Compatível|Não compatível com [3]|  
  
 [1], o aplicativo deve recompilar usando cabeçalhos ODBC 3.5 (ou superior) com a opção de UNICODE (se for um aplicativo Unicode) e configure ODBCVER para 0x0250.  
  
 [2], o aplicativo deve compilar o uso de cabeçalhos ODBC 3.5 (ou superior) e vincular com o Gerenciador de Driver ODBC. Ele também deve definir o sinalizador de cabeçalho ODBC_STD.  
  
 [3] essa configuração potencialmente pode não funcionar porque há recursos do ODBC 2. *x* que não estão com os padrões, como marcadores.  
  
 [4] esta configuração potencialmente pode não funcionar porque há recursos no ODBC 3 *. x* que não estão com os padrões, como marcadores.  
  
 [5] essa configuração pode potencialmente falhar porque há recursos que não estão no ODBC 2.x ou 3.x drivers, como específicos de driver no ODBC 3.8 [tipos de dados C em ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
## <a name="driver-manager-compatibility"></a>Compatibilidade do Gerenciador de driver  
 Um aplicativo ODBC 3.0 que deve funcionar com todas as versões do Gerenciador de Driver deve fazer o seguinte na inicialização:  
  
-   Alocar um identificador de ambiente.  
  
-   Defina o atributo de ambiente de SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3_80. Se o Gerenciador de Driver retornará SQL_ERROR, o Gerenciador de Driver é anterior ao 3.8. Redefina SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC3 ou SQL_OV_ODBC2, conforme apropriado, para corresponder ao Gerenciador de Driver.  
  
-   Alocar um identificador de conexão.  
  
-   Fazer uma conexão.  
  
-   Chame SQLGetInfo para SQL_DRIVER_ODBC_VER determinar a versão do driver. Se o driver é um driver de ODBC 3.8, você pode usar tipos do C específicos do driver. Caso contrário, não use tipos de dados C específicos do driver.  
  
 Observe que um aplicativo de 3. x recompilado ODBC pode usar recursos de ODBC 3.8 diferentes tipos de C específicos do driver sem especificar SQL_OV_ODBC3_80 para SQL_ATTR_ODBC_VERSION. Isso é semelhante a um aplicativo recompilado ODBC 2.x usando os recursos do ODBC 3. x.  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>Usando SQLCancelHandle de um aplicativo compatível com todos os gerenciadores de Driver  
 Porque [função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) não tem suporte em gerenciadores de Driver que foram lançadas antes do Windows 7, um aplicativo não pode ser carregado em versões anteriores do Windows se chama **SQLCancelHandle** diretamente. Para trabalhar com todas as versões do Driver de gerentes e usar **SQLCancelHandle** em novas versões do Windows, um aplicativo deve chamar **SQLCancelHandle** indiretamente usando **LoadLibrary** e **GetProcAddress.**  
  
## <a name="see-also"></a>Consulte também  
 [Novidades no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
