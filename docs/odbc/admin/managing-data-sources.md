---
title: Gerenciando fontes de dados | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a5069ac9a5babc3071c52d73d5b56b21729a5d8a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307207"
---
# <a name="managing-data-sources"></a>Gerenciar fontes de dados
Depois de instalar um driver ODBC do programa de instalação do driver, você pode definir uma ou mais fontes de dados para ele. O nome da fonte de dados (DSN) deve fornecer uma descrição exclusiva dos dados; por exemplo, *folha de pagamento* ou *contas a pagar*. As fontes de dados do usuário e do sistema definidas para todos os drivers instalados atualmente são listadas nas guias **DSN do usuário** ou **DSN do sistema** da caixa de diálogo administrador de **fonte de dados ODBC** . As fontes de dados de arquivo em um determinado diretório são listadas na guia **DSN de arquivo** ; o diretório a ser mostrado é inserido na caixa **examinar** na guia DSN de **arquivo** .  
  
> [!NOTE]  
>  Para gerenciar uma fonte de dados que se conecta a um driver de 32 bits na plataforma de 64 bits, use c:\windows\sysWOW64\odbcad32.exe. Para gerenciar uma fonte de dados que se conecta a um driver de 64 bits, use c:\windows\system32\odbcad32.exe. Em **Ferramentas administrativas** em um sistema operacional Windows 8 de 64 bits, há ícones para a caixa de diálogo **administrador de fonte de dados ODBC** de 32 bits e 64 bits.  
  
 Se você usar o odbcad32. exe de 64 bits para configurar ou remover um DSN que se conecta a um driver de 32 bits, por exemplo, **Driver do Microsoft Access\*(. mdb)**, você receberá a seguinte mensagem de erro:  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 Para resolver esse erro, use o odbcad32. exe de 32 bits para configurar ou remover o DSN.  
  
 Uma fonte de dados associa um driver ODBC específico aos dados que você deseja acessar por meio desse driver. Por exemplo, você pode criar uma fonte de dados para usar o driver do dBASE do ODBC para acessar um ou mais arquivos do dBASE encontrados em um diretório específico no disco rígido ou em uma unidade de rede. Usando o administrador de fonte de dados ODBC, você pode adicionar, modificar e excluir fontes de dados, conforme descrito na tabela a seguir.  
  
|Ação|Descrição|  
|------------|-----------------|  
|Adicionando fontes de dados|É possível adicionar várias fontes de dados, cada uma associando um driver a alguns dados que você deseja acessar usando esse driver. Dê a cada fonte de dados um nome que identifique exclusivamente essa fonte de dados. Por exemplo, se você criar uma fonte de dados para um conjunto de arquivos do dBASE que contêm informações do cliente, poderá nomear a fonte de dados como "Customers". Os aplicativos normalmente exibem nomes de fontes de dados para os usuários escolherem.<br /><br /> A adição de uma fonte de dados de arquivo é ligeiramente diferente da adição de fontes de dados do usuário ou do sistema. Para obter mais informações, consulte o arquivo de ajuda do administrador de fonte de dados ODBC.|  
|Modificando fontes de dados|Dependendo dos seus requisitos, talvez você ache necessário reconfigurar as fontes de dados. Você pode redefinir opções clicando em **Configurar** em qualquer configuração de driver caixa de diálogo.|  
|Excluindo fontes de dados|Clique em **remover** depois de selecionar uma fonte de dados.|  
  
 Para obter mais informações sobre fontes de dados de arquivo, consulte [conectar-se usando fontes de dados de arquivo](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) ou a [função SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Administrador de fonte de dados ODBC](../../odbc/admin/odbc-data-source-administrator.md)
