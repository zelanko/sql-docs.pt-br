---
title: Matriz de Compatibilidade | Microsoft Docs
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
ms.openlocfilehash: 0406599e1657a900d1669861572ff13834cec670
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307449"
---
# <a name="compatibility-matrix"></a>Matriz de compatibilidade
A tabela a seguir descreve a compatibilidade dos tipos de aplicativos e drivers definidos anteriormente nesta seção.  
  
|Tipo de aplicativo<br /><br /> e versão|ODBC de 32 bits<br /><br /> *Driver 2.x*|ODBC *3.x*<br /><br /> Driver|Driver ODBC 3.8|Driver compatível com ISO e Open Group|  
|--------------------------------------|-----------------------------------|---------------------------|---------------------|-----------------------------------------|  
|Aplicativo de 16 bits, qualquer versão|Compatível|Compatível|Compatível|Compatível|  
|Aplicação *pura 2.x*|Compatível|Compatível|Compatível|Não compatível[3]|  
|Aplicativo recompilado puro *2.x*|Compatível|Compatível[1]|Compatível[1]|Não compatível[3]|  
|Aplicativo Unicode *puro 2.x*|Compatível|Compatível[1]|Compatível[1]|Não compatível[3]|  
|Aplicativo compatível com Pure Open Group e ISO|Não compatível|Compatível[2]|Compatível[2]|Compatível[2]|  
|Aplicação Pure 3.0|Não compatível|Compatível|Compatível|Não compatível[4]|  
|Aplicação pura 3.5|Não compatível|Compatível|Compatível|Não compatível[4]|  
|Aplicação pura 3.8 (ou superior)|Não compatível [5]|Não compatível [5]|Compatível|Não compatível [4]|  
|Aplicativo substituído|Compatível|Compatível|Compatível|Não compatível[3]|  
  
 [1] O aplicativo deve recompilar usando cabeçalhos ODBC 3.5 (ou superior) com a opção UNICODE (se for um aplicativo Unicode) e deve definir ODBCVER como 0x0250.  
  
 [2] O aplicativo deve compilar usando cabeçalhos ODBC 3.5 (ou superior) e vincular-se ao Gerenciador de Driver oDBC. Também deve definir a bandeira de cabeçada ODBC_STD.  
  
 [3] Essa configuração pode potencialmente não funcionar porque existem recursos no ODBC *2.x* que não estão nos padrões, como marcadores.  
  
 [4] Essa configuração pode potencialmente não funcionar porque existem recursos no ODBC *3.x* que não estão nos padrões, como marcadores.  
  
 [5] Essa configuração pode potencialmente falhar porque existem recursos no ODBC 3.8 que não estão em drivers ODBC 2.x ou 3.x, como os tipos de dados C específicos do driver [no ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
## <a name="driver-manager-compatibility"></a>Compatibilidade com o gerenciador de drivers  
 Um aplicativo ODBC 3.0 que deve operar com todas as versões do Driver Manager deve fazer o seguinte na inicialização:  
  
-   Aloque uma alça de ambiente.  
  
-   Defina o SQL_ATTR_ODBC_VERSION atributo ambiental para SQL_OV_ODBC3_80. Se o Driver Manager retornar SQL_ERROR, o Driver Manager é mais velho que 3,8. Redefinir SQL_ATTR_ODBC_VERSION para SQL_OV_ODBC3 ou SQL_OV_ODBC2, conforme apropriado, corresponder ao Driver Manager.  
  
-   Aloque uma alça de conexão.  
  
-   Faça uma conexão.  
  
-   Ligue para o SQLGetInfo para SQL_DRIVER_ODBC_VER para determinar a versão do driver. Se o driver for um driver ODBC 3.8, você pode usar os tipos C específicos do motorista. Caso contrário, não use os tipos de dados C específicos do driver.  
  
 Observe que um aplicativo ODBC 3.x recompilado pode usar recursos ODBC 3.8 que não são tipos C específicos do driver, sem especificar SQL_OV_ODBC3_80 para SQL_ATTR_ODBC_VERSION. Isso é semelhante a um aplicativo ODBC 2.x recompilado usando recursos ODBC 3.x.  
  
## <a name="using-sqlcancelhandle-in-an-application-compatible-with-all-driver-managers"></a>Usando sqlcancelhandle em um aplicativo compatível com todos os gerentes de driver  
 Como [a função SQLCancelHandle](../../../odbc/reference/syntax/sqlcancelhandle-function.md) não é suportada nos gerentes de driver que foram lançados antes do Windows 7, um aplicativo não pode ser carregado em versões mais antigas do Windows se ele chamar **SQLCancelHandle** diretamente. Para trabalhar com todas as versões dos driver managers e usar **o SQLCancelHandle** em novas versões do Windows, um aplicativo deve chamar **SQLCancelHandle** indiretamente usando **LoadLibrary** e **GetProcAddress.**  
  
## <a name="see-also"></a>Consulte Também  
 [Novidades no ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
