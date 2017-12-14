---
title: Conectar-se a um dBASE ou a outro arquivo DBF | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connecting to DBF files
- dBase files
- DBF files
ms.assetid: b0e8c831-9f96-475c-82a4-4f5b02692752
caps.latest.revision: "16"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 60fc92f8283ec9b4952152aca6b1e0a5d31a1e6d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="connect-to-a-dbase-or-other-dbf-file"></a>Conectar-se a um dBASE ou a outro arquivo DBF
  Você pode conectar-se a um dBASE ou a outro arquivo de banco de dados .DBF em um pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usando um gerenciador de conexões do OLE DB e selecionando a opção Microsoft OLE DB Provider for Jet 4.0.  
  
> [!NOTE]  
>  O Assistente de Importação e Exportação do SQL Server no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte à importação ou exportação a partir do dBASE ou outros arquivos .DBF. Você pode usar o Microsoft Access ou o Microsoft Excel para importar os dados dos arquivos .DBF para um banco de dados do Access ou planilhas do Excel e usar o Assistente de Importação e Exportação do SQL Server.  
  
### <a name="to-configure-a-connection-manager-to-connect-to-a-dbase-or-other-dbf-file"></a>Configurar um gerenciador de conexões para estabelecer conexão com um dBASE ou outro arquivo .DBF  
  
1.  Adicione um novo gerenciador de conexões do OLE DB ao pacote. Para obter mais informações, consulte [Add, Delete, or Share a Connection Manager in a Package](http://msdn.microsoft.com/library/6f2ba4ea-10be-4c40-9e80-7efcf6ee9655).  
  
2.  Na página **Conexão** da caixa de diálogo **Gerenciador de Conexões** , selecione OLE DB Nativo\Provedor OLE DB do Microsoft Jet 4.0 como o **Provedor**.  
  
3.  Ao trabalhar com arquivos .DBF, a pasta representa o banco de dados e os arquivos .DBF individuais representam as tabelas. Por isso, a caixa de texto **Nome do arquivo de banco de dados** deve conter o caminho da pasta em que estão os arquivos .DBF e não deve incluir o nome do próprio arquivo. Você pode digitar ou colar em um caminho da pasta ou usar o botão **Procurar** para selecionar seu arquivos .DBF e remover o nome do arquivo do final do caminho da pasta.  
  
4.  Na página **Tudo** da caixa de diálogo **Gerenciador de Conexões** , insira **dBASE III**, **dBASE IV**ou **dBASE 5.0**, conforme apropriado, como o valor de Propriedades Estendidas.  
  
5.  Clique em **Conexão de Teste** para validar os valores que você inseriu. A mensagem "Conexão de teste bem-sucedida" deve ser exibida. Clique em **OK** para fechar a caixa de mensagens.  
  
6.  Clique em **OK** para salvar a configuração do gerenciador de conexões.  
  
7.  Para usar o gerenciador de conexões no fluxo de dados do pacote, selecione uma origem ou um destino de OLE DB e configure-o para usar o gerenciador de conexões que você criou usando as etapas anteriores.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de conexões OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)  
  
  
