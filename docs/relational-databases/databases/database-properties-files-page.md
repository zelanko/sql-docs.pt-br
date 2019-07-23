---
title: Propriedades do banco de dados (página Arquivos) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.files.f1
ms.assetid: 3c030e51-db82-4b43-b1e5-8547ddd3de87
author: stevestein
ms.author: sstein
ms.openlocfilehash: f3c0493192381bc3dedbf23ab1e01c0142e88be4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68099615"
---
# <a name="database-properties-files-page"></a>Propriedades do Banco de Dados (página Arquivos)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use esta página para criar um novo banco de dados ou para exibir ou modificar as propriedades do banco de dados selecionado. Este tópico se aplica às **Propriedades do Banco de Dados (página Arquivos)** de bancos de dados existentes e ao **Novo Banco de Dados (página Geral)** .  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Nome do banco de dados**  
 Adicione ou exiba o nome do banco de dados.  
  
 **Proprietário**  
 Especifique o proprietário do banco de dados selecionando na lista.  
  
 **Usar indexação de texto completo**  
 Essa caixa de seleção fica marcada e desabilitada porque a indexação de texto completo está sempre habilitada no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, consulte [Pesquisa de texto completo](../../relational-databases/search/full-text-search.md).  
  
 **Arquivos do banco de dados**  
 Adicione, exiba, modifique ou remova arquivos do banco de dados associado. Arquivos de banco de dados têm as seguintes propriedades:  
  
 **Nome Lógico**  
 Digite ou modifique o nome do arquivo.  
  
 **Tipo de arquivo**  
 Selecione o tipo de arquivo na lista. O tipo de arquivo pode ser **Dados**, **Log**ou **Dados de Filestream**. Você não pode modificar o tipo de arquivo de um arquivo existente.  
  
 Selecione **Dados do Fluxo de Arquivos** se estiver adicionando arquivos (contêineres) a um grupo de arquivos com otimização de memória.  
  
 Para adicionar arquivos (contêineres) a um grupo de arquivos de dados de Filestream, o FILESTREAM deve estar habilitado. Você pode habilitar o FILESTREAM usando a caixa de diálogo [Propriedades do Servidor (página Avançado)](../../database-engine/configure-windows/server-properties-advanced-page.md) .  
  
 **Grupo de arquivos**  
 Selecione o grupo de arquivos do arquivo na lista. Por padrão, o grupo de arquivos é PRIMARY. É possível criar um novo grupo de arquivos selecionando **\<novo grupo de arquivos>** e inserindo informações sobre ele na caixa de diálogo **Novo grupo de arquivos**. Um novo grupo de arquivos também pode ser criado na página **Grupo de Arquivos** . Você não pode modificar o grupo de arquivos de um arquivo existente.  
  
 Ao adicionar arquivos (contêineres) a um grupo de arquivos com otimização de memória, o campo de **Grupo de Arquivos** será preenchido com o nome do grupo de arquivos com otimização de memória do banco de dados.  
  
 **Tamanho Inicial**  
 Digite ou modifique o tamanho inicial do arquivo em megabytes. Por padrão, esse é o valor do banco de dados **modelo** .  
  
 Esse campo não é válido para arquivos de FILESTREAM.  
  
 Para arquivos em grupos de arquivos com otimização de memória, este campo não pode ser alterado.  
  
 **Aumento Automático**  
 Selecione ou exiba as propriedades de aumento automático do arquivo. Essas propriedades controlam como o arquivo se expande quando seu tamanho máximo é alcançado. Para editar valores de aumento automático, clique no botão de edição ao lado das propriedades de aumento automático do arquivo desejado e altere os valores na caixa de diálogo **Alterar Aumento Automático** . Por padrão, esses são os valores do banco de dados **modelo** .  
  
 Esse campo não é válido para arquivos de FILESTREAM.  
  
 Para arquivos em grupos de arquivos com otimização de memória, este campo deve ser **Ilimitado**.  
  
 **Caminho**  
 Exibe o caminho do arquivo selecionado. Para especificar um caminho para um novo arquivo, clique no botão de edição próximo ao caminho do arquivo e navegue até a pasta de destino. Você não pode modificar o caminho de um arquivo existente.  
  
 Para arquivos de FILESTREAM, o caminho é uma pasta. O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] criará os arquivos subjacentes nesta pasta.  
  
 **Nome do Arquivo**  
 Exibe o nome do arquivo.  
  
 Este campo não é válido para arquivos de FILESTREAM, incluindo arquivos em grupos de arquivos com otimização de memória.  
  
 **Adicionar**  
 Adicione um novo arquivo ao banco de dados.  
  
 **Remover**  
 Exclua o arquivo selecionado do banco de dados. Um arquivo não pode ser removido, a menos que esteja vazio. O arquivo de dados principal e o arquivo de log não podem ser removidos.  
  
 Para obter informações sobre arquivos, consulte [Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md).  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
  
