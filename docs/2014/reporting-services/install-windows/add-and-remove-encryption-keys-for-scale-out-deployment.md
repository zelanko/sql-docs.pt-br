---
title: Adicionar e remover chaves de criptografia para implantação de expansão (Gerenciador de configuração do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- encryption keys [Reporting Services]
- deleting encryption keys
- removing encryption keys
- adding encryption keys
- rskeymgmt utility
- scale-out deployments [Reporting Services]
ms.assetid: 2da86fb3-4b4d-407f-9825-74dcc42486f5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 52ecac095d34882d8f65cdafaa83784aef86e2fc
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59967902"
---
# <a name="add-and-remove-encryption-keys-for-scale-out-deployment-ssrs-configuration-manager"></a>Adicionar e remover chaves de criptografia para implantação em expansão (Gerenciador de configurações do SSRS)
  É possível executar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em um modelo de implantação de expansão com a configuração de vários servidores de relatório para usarem um banco de dados do servidor de relatório compartilhado. A associação em uma implantação de expansão tem como base o fato de o servidor de relatório armazenar uma chave de criptografia no banco de dados do servidor de relatório. Você pode controlar a associação de implantação de expansão pela adição ou remoção de chaves de criptografia para instâncias específicas do servidor de relatório. Se estiver removendo nós da implantação, você poderá os removê-los em qualquer ordem. Se estiver adicionando nós a uma implantação, você deverá unir quaisquer novas instâncias de um servidor de relatório que já faça parte da implantação.  
  
## <a name="using-the-reporting-services-configuration-tool-to-configure-scale-out-deployment"></a>Usando a ferramenta Configuração do Reporting Services para configurar a implantação de expansão  
 O modo mais fácil para configurar uma implantação de expansão é usar a ferramenta Configuração do Reporting Services. Para obter mais informações e instruções passo a passo, consulte [Configurar uma implantação em expansão do servidor de relatório em modo nativo &#40;SSRS Configuration Manager&#41;](configure-a-native-mode-report-server-scale-out-deployment.md).  
  
## <a name="using-rskeymgmt-to-configure-scale-out-deployment"></a>Usando Rskeymgmt para configurar a implantação de expansão  
 Use o utilitário **rskeymgmt** para inicializar uma instância do servidor de relatório a fim de usar um banco de dados de servidor de relatório compartilhado. A adição de um servidor de relatório para uma implantação de expansão exige que você inicialize o servidor de relatório. A inicialização exige permissões de administrador. Você deve ter credenciais de administrador para o computador remoto que hospeda o servidor de relatório que está sendo associado à implantação.  
  
#### <a name="how-to-join-a-report-server-to-a-scale-out-deployment-rskeymgmt"></a>Como unir um servidor de relatório a uma implantação de expansão (rskeymgmt)  
  
1.  Execute **rskeymgmt.exe** localmente no computador que hospeda um servidor de relatório que já seja um membro da implantação de expansão do servidor de relatório.  
  
2.  Use o argumento `-j` para unir um servidor de relatório ao banco de dados do servidor de relatório. Use os argumentos `-m` e `-n` para especificar a instância do servidor de relatório remoto que deseja adicionar à implantação. Use os argumentos `-u` e `-v` para especificar uma conta de administrador no computador remoto. Se estiver criando uma implantação de expansão com o uso de várias instâncias de servidor de relatório no mesmo computador, a sintaxe a ser usada é um pouco diferente. Para obter mais informações sobre a sintaxe que deve ser usada, consulte [Utilitário rskeymgmt &#40;SSRS&#41;](../tools/rskeymgmt-utility-ssrs.md).  
  
     O exemplo a seguir ilustra os argumentos que devem ser especificados se você estiver associando um servidor de relatório remoto a uma implantação de expansão (essas credenciais podem ser omitidas se você tiver permissões de administrador no computador remoto):  
  
    ```  
    rskeymgmt -j -m <remotecomputer> -n <namedreportserverinstance> -u <administratoraccount> -v <administratorpassword>  
    ```  
  
#### <a name="how-to-remove-a-report-server-from-a-scale-out-deployment-rskeymgmt"></a>Como remover um servidor de relatório de uma implantação de expansão (rskeymgmt)  
  
1.  Abra o arquivo rsreportserver.config do servidor de relatório que deseja remover e localize o ID da instalação. Por padrão, esse arquivo está localizado em Arquivos de Programas\Microsoft SQL Server\MSSQL.*n*\Reporting Services\ReportServer).  
  
     Se você instalou uma única instância, haverá apenas um arquivo rsreportserver.config no computador. Se várias instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] estiverem instaladas, use a página Status do Servidor na ferramenta Configuração do Reporting Services para localizar o identificador da instância (por exemplo, MSSQL.2) do servidor de relatório que deseja remover. O nome da pasta que armazena os arquivos de programas da instância do servidor de relatório terá como base o identificador da instância (por exemplo, Arquivos de Programas\Microsoft SQL Server\MSSQL.2).  
  
2.  Execute **rskeymgmt.exe**. Isso pode ser executado em qualquer servidor de relatório que faça parte da implantação de expansão do servidor de relatório.  
  
3.  Use o argumento `-r` para liberar a instância do servidor de relatório da implantação de expansão. O exemplo a seguir ilustra os argumentos que você deve especificar:  
  
    ```  
    rskeymgmt -r <installation ID>  
    ```  
  
 Essas etapas removem o servidor de relatório de uma implantação em expansão, mas não desinstalam a instância do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no servidor de relatório. Depois de remover o servidor de relatório da implantação em expansão, você pode desinstalar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do servidor de relatório se não precisar mais do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nesse servidor. Para obter informações, consulte [Desinstalar uma instância existente do SQL Server &#40;Instalação&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md) nos Manuais online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte também  
 [Configurar e gerenciar chaves de criptografia &#40;SSRS Configuration Manager&#41;](ssrs-encryption-keys-manage-encryption-keys.md)   
 [Inicializar um servidor de relatório &#40;SSRS Configuration Manager&#41;](ssrs-encryption-keys-initialize-a-report-server.md)  
  
  
