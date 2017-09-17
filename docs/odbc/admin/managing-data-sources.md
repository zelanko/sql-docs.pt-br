---
title: Gerenciar fontes de dados | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting data sources [ODBC], ODBC data source administrator
- data sources [ODBC], ODBC data source administrator
- adding data sources [ODBC], ODBC data source administrator
- removing data sources [ODBC], ODBC data source administrator
- ODBC data source administrator [ODBC], data source management
ms.assetid: 67cc4945-4850-4eb4-8da6-b835ddaeca4c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d80594ac41f27d28051fc64f489b5cad59335c00
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="managing-data-sources"></a>Gerenciar fontes de dados
Depois de instalar um driver ODBC do programa de instalação do driver, você pode definir uma ou mais fontes de dados para ele. O nome da fonte de dados (DSN) deve fornecer uma descrição exclusiva dos dados. Por exemplo, *folha de pagamento* ou *contas a pagar*. As fontes de dados de usuário e do sistema que estão definidas para todos os drivers instalados no momento são listadas no **DSN do usuário** ou **DSN de sistema** guias do **administrador de fonte de dados ODBC**caixa de diálogo. As fontes de dados de arquivo em um diretório específico são listadas no **DSN de arquivo** guia; o diretório a ser mostrado é inserido no **examinar** caixa o **DSN de arquivo** guia.  
  
> [!NOTE]  
>  Para gerenciar uma fonte de dados que se conecta a um driver de 32 bits em plataformas de 64 bits, use c:\windows\sysWOW64\odbcad32.exe. Para gerenciar uma fonte de dados que se conecta a um driver de 64 bits, use c:\windows\system32\odbcad32.exe. Em **ferramentas administrativas** em um sistema de operacional do Windows 8 de 64 bits, há ícones para 32 bits e 64 bits **administrador de fonte de dados ODBC** caixa de diálogo.  
  
 Se você usar o odbcad32.exe 64-bit para configurar ou remover um DSN que se conecta a um driver de 32 bits, por exemplo, **Driver Microsoft Access (\*. mdb)**, você receberá a seguinte mensagem de erro:  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 Para resolver esse erro, use o odbcad32.exe 32 bits para configurar ou remover o DSN.  
  
 Uma fonte de dados associa um determinado driver ODBC com os dados que você deseja acessar pelo driver. Por exemplo, você pode criar uma fonte de dados para usar o driver ODBC do dBASE para acessar um ou mais arquivos dBASE encontrados em um diretório específico no disco rígido ou uma unidade de rede. Usando o administrador de fonte de dados ODBC, você pode adicionar, modificar e excluir fontes de dados, conforme descrito na tabela a seguir.  
  
|Ação|Description|  
|------------|-----------------|  
|Adicionando fontes de dados|É possível adicionar várias fontes de dados, cada uma associação de um driver com alguns dados que você deseja acessar usando o driver. Dê um nome que identifica exclusivamente essa fonte de dados de cada fonte de dados. Por exemplo, se você criar uma fonte de dados para um conjunto de arquivos dBASE que contêm informações de cliente, você pode nomear a fonte de dados "Clientes". Aplicativos normalmente exibem nomes de fonte de dados para os usuários à sua escolha.<br /><br /> Adicionando uma fonte de dados de arquivo é ligeiramente diferente da adição de fontes de dados do sistema ou usuário. Para obter mais informações, consulte o administrador de fonte de dados ODBC no arquivo de Ajuda.|  
|Modificando fontes de dados|Dependendo dos requisitos, talvez seja necessário reconfigurar as fontes de dados. Você pode redefinir as opções clicando **configurar** em qualquer caixa de diálogo de instalação do driver.|  
|Excluindo fontes de dados|Clique em **remover** depois de selecionar uma fonte de dados.|  
  
 Para obter mais informações sobre fontes de dados de arquivo, consulte [conectar fontes de dados de arquivo usando](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) ou [função SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Consulte também  
 [Administrador de fonte de dados ODBC](../../odbc/admin/odbc-data-source-administrator.md)
