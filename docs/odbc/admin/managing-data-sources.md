---
title: Gerenciar fontes de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- deleting data sources [ODBC], ODBC data source administrator
- data sources [ODBC], ODBC data source administrator
- adding data sources [ODBC], ODBC data source administrator
- removing data sources [ODBC], ODBC data source administrator
- ODBC data source administrator [ODBC], data source management
ms.assetid: 67cc4945-4850-4eb4-8da6-b835ddaeca4c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6a1f8893351ceb68ebd7c42e3ac82c876c01c10b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198758"
---
# <a name="managing-data-sources"></a>Gerenciar fontes de dados
Depois de instalar um driver ODBC do programa de instalação do driver, você pode definir uma ou mais fontes de dados para ele. O nome da fonte de dados (DSN) deve fornecer uma descrição exclusiva dos dados. Por exemplo, *folha de pagamento* ou *contas a pagar*. As fontes de dados de usuário e do sistema que são definidas para todos os drivers instalados no momento são listadas na **DSN de usuário** ou **DSN de sistema** guias do **administrador de fonte de dados ODBC**caixa de diálogo. As fontes de dados de arquivo em um determinado diretório são listadas na **DSN de arquivo** guia; o diretório a ser mostrado é inserido na **examinar** caixa a **DSN de arquivo** guia.  
  
> [!NOTE]  
>  Para gerenciar uma fonte de dados que se conecta a um driver de 32 bits na plataforma de 64 bits, use c:\windows\sysWOW64\odbcad32.exe. Para gerenciar uma fonte de dados que se conecta a um driver de 64 bits, use c:\windows\system32\odbcad32.exe. Na **ferramentas administrativas** em um sistema de operacional do Windows 8 de 64 bits, há ícones para os 32 bits e 64 bits **administrador de fonte de dados ODBC** caixa de diálogo.  
  
 Se você usar o odbcad32.exe 64-bit para configurar ou remover um DSN que se conecta a um driver de 32 bits, por exemplo, **Driver Microsoft Access (\*. mdb)**, você receberá a seguinte mensagem de erro:  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 Para resolver esse erro, use o odbcad32.exe 32 bits para configurar ou remover o DSN.  
  
 Uma fonte de dados associa um determinado driver ODBC com os dados que você deseja acessar por meio do driver. Por exemplo, você pode criar uma fonte de dados para usar o driver do dBASE ODBC para acessar um ou mais arquivos dBASE encontrados em um diretório específico no seu disco rígido ou uma unidade de rede. Usando o administrador de fonte de dados ODBC, você pode adicionar, modificar e excluir fontes de dados, conforme descrito na tabela a seguir.  
  
|Ação|Descrição|  
|------------|-----------------|  
|Adicionando fontes de dados|É possível adicionar várias fontes de dados, cada um deles associando um driver com alguns dados que você deseja acessar usando esse driver. Dê um nome que identifica exclusivamente essa fonte de dados de cada fonte de dados. Por exemplo, se você criar uma fonte de dados para um conjunto de arquivos dBASE que contêm informações do cliente, você pode nomear a fonte de dados "Clientes". Aplicativos normalmente exibem nomes de fonte de dados para os usuários podem escolher.<br /><br /> Adicionando uma fonte de dados de arquivo é um pouco diferente da adição de usuário ou fontes de dados do sistema. Para obter mais informações, consulte o administrador de fonte de dados ODBC no arquivo de Ajuda.|  
|Modificando fontes de dados|Dependendo dos seus requisitos, talvez seja necessário reconfigurar as fontes de dados. Você pode redefinir opções clicando **configurar** em qualquer caixa de diálogo de instalação do driver.|  
|Excluindo fontes de dados|Clique em **remover** depois de selecionar uma fonte de dados.|  
  
 Para obter mais informações sobre fontes de dados de arquivo, consulte [conectar fontes de dados de arquivo usando](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) ou o [função SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Consulte também  
 [Administrador de fonte de dados ODBC](../../odbc/admin/odbc-data-source-administrator.md)
