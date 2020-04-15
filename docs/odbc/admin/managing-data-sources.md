---
title: Gerenciamento de fontes de dados | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307207"
---
# <a name="managing-data-sources"></a>Gerenciar fontes de dados
Depois de instalar um driver ODBC no programa de configuração do driver, você pode definir uma ou mais fontes de dados para ele. O nome de origem dos dados (DSN) deve fornecer uma descrição única dos dados; por exemplo, *Folha de pagamento* ou contas a *pagar.* As fontes de dados do usuário e do sistema definidas para todos os drivers instalados atualmente estão listadas nas guias **DSN** do Usuário ou **do Sistema DSN** da caixa de diálogo Administrador de Origem de **Dados oDBC.** As fontes de dados do arquivo em um determinado diretório estão listadas na guia **Arquivo DSN;** o diretório a ser mostrado é inserido na caixa **Olhar na** caixa na guia **Arquivo DSN.**  
  
> [!NOTE]  
>  Para gerenciar uma fonte de dados que se conecta a um driver de 32 bits em uma plataforma de 64 bits, use c:\windows\sysWOW64\odbcad32.exe. Para gerenciar uma fonte de dados que se conecta a um driver de 64 bits, use c:\windows\system32\odbcad32.exe. Em **Ferramentas Administrativas** em um sistema operacional Windows 8 de 64 bits, existem ícones para a caixa de diálogo **Administrador de Código de Dados ODBC** de 32 bits e 64 bits.  
  
 Se você usar o odbcad32.exe de 64 bits para configurar ou remover um DSN que se conecta a um driver de 32 bits, por exemplo, **Driver do Microsoft Access (.mdb)\***, você receberá a seguinte mensagem de erro:  
  
```  
The specified DSN contains an architecture mismatch between the Driver and Application  
```  
  
 Para resolver esse erro, use o odbcad32.exe de 32 bits para configurar ou remover o DSN.  
  
 Uma fonte de dados associa um driver ODBC particular com os dados que você deseja acessar através desse driver. Por exemplo, você pode criar uma fonte de dados para usar o driver oDBC dBASE para acessar um ou mais arquivos dBASE encontrados em um diretório específico em seu disco rígido ou em uma unidade de rede. Usando o Administrador de Origem de Dados do ODBC, você pode adicionar, modificar e excluir fontes de dados, conforme descrito na tabela a seguir.  
  
|Ação|Descrição|  
|------------|-----------------|  
|Adicionando fontes de dados|É possível adicionar várias fontes de dados, cada uma associando um driver a alguns dados que você deseja acessar usando esse driver. Dê a cada fonte de dados um nome que identifique exclusivamente essa fonte de dados. Por exemplo, se você criar uma fonte de dados para um conjunto de arquivos dBASE que contenham informações do cliente, você pode nomear a fonte de dados "Clientes". Os aplicativos normalmente exibem nomes de origem de dados para os usuários escolherem.<br /><br /> Adicionar uma fonte de dados de arquivo é ligeiramente diferente de adicionar fontes de dados de usuário ou sistema. Para obter mais informações, consulte o arquivo de ajuda do Administrador de Origem de Dados oDBC.|  
|Modificando fontes de dados|Dependendo de suas necessidades, você pode achar necessário reconfigurar fontes de dados. Você pode redefinir as opções clicando em **Configurar** em qualquer caixa de diálogo de configuração do driver.|  
|Exclusão de fontes de dados|Clique **em Remover** depois de selecionar uma fonte de dados.|  
  
 Para obter mais informações sobre fontes de dados de arquivos, consulte [Conectar-se usando fontes de dados de arquivo](../../odbc/reference/develop-app/connecting-using-file-data-sources.md) ou a função [SQLDriverConnect](../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Administrador de fonte de dados ODBC](../../odbc/admin/odbc-data-source-administrator.md)
