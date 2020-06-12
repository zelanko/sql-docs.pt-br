---
title: Geral (caixa de diálogo Restore Database) (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.restoredbdialog.f1
ms.assetid: 319e7ef5-c9c7-4e50-8690-02a90aed006f
author: minewiskan
ms.author: owend
ms.openlocfilehash: 787488570627e2c8c7fc9a37e8f814847c40f3ca
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544378"
---
# <a name="general-restore-database-dialog-box-analysis-services---multidimensional-data"></a>Geral (caixa de diálogo Restaurar Banco de Dados) (Analysis Services - Dados multidimensionais)
  Use a página **Geral** da caixa de diálogo **Restaurar Banco de Dados** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para especificar o arquivo de backup e configurações gerais para usar ao restaurar um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Para cada arquivo de backup, o usuário que executar o comando de restauração deve ter permissão para ler no local de backup especificado para cada arquivo. Para restaurar um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que não esteja instalado no servidor, o usuário também deve ser membro da função de servidor dessa instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Para substituir um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , o usuário deve ter uma das seguintes funções: membro da função de servidor da instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle Total (Administrador) no banco de dados a ser restaurado.  
  
> [!NOTE]  
>  Após restaurar um banco de dados existente, o usuário que o restaurou poderá perder o acesso ao banco de dados restaurado. Essa perda de acesso pode ocorrer se, no momento da execução do backup, o usuário não for membro da função de servidor, nem membro da função de banco de dados com permissões de Controle total (Administrador).  
  
 **Para exibir a página Geral na caixa de diálogo Restaurar Banco de Dados**  
  
-   No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse na pasta **Bancos de Dados** de uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou em um banco de dados no **Pesquisador de Objetos**, clique em **Restaurar**e então, em **Selecionar uma página**, clique em **Geral**.  
  
## <a name="options"></a>Opções  
 **Script**  
 Cria um script de restauração baseado nas opções selecionadas na caixa de diálogo. O script de restauração é escrito na Linguagem de Scripts do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] (ASSL).  
  
 Clicar no ícone **Script** envia o script de restauração a uma nova janela de consulta, por padrão.  
  
 Clicar na seta **Script** exibe um menu que permite escolher para onde enviar o script de restauração:  
  
-   Para uma nova janela de consulta (padrão).  
  
-   Para um arquivo.  
  
-   Para a área de transferência.  
  
-   Para um trabalho.  
  
 **Restaurar banco de dados**  
 Selecione o banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] a restaurar.  
  
 **De arquivo de backup**  
 Selecione o arquivo de backup do qual restaurar o banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] selecionado.  
  
 **Procurar**  
 Clique para exibir a caixa de diálogo **Localizar Arquivos de Banco de Dados** e selecionar o caminho e nome do arquivo de backup a utilizar. Para obter mais informações sobre a caixa de diálogo **Localizar Arquivos de Banco de Dados**, consulte [Caixa de diálogo Localizar Arquivos de Banco de Dados &#40;Analysis Services – Dados Multidimensionais&#41;](locate-database-files-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Permitir substituição de banco de dados**  
 Selecione para permitir que o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] restaure os conteúdos do arquivo de backup selecionado em lugar de quaisquer objetos existentes no banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] selecionado.  
  
 **Incluir informações de segurança**  
 Selecione para copiar quaisquer informações de segurança armazenadas no arquivo de backup para o banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 Se esta opção for selecionada, você poderá escolher a quantidade de informações de segurança na lista suspensa habilitada ao selecionar esta opção. As seguintes opções estão disponíveis:  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Copiar tudo**|Restaura as funções de banco de dados contidas no arquivo de backup, assim como as contas de usuário associadas às funções.|  
|**Ignorar Associação**|Restaura as funções de banco de dados contidas no arquivo de backup, mas não restaura as contas de usuário associadas às funções.|  
  
 **Senha**  
 Se o arquivo de backup estiver criptografado, digite a senha usada para criptografar o arquivo de backup.  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo Restaurar Banco de dados &#40;Analysis Services-&#41;](restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Caixa de diálogo partições &#40;Restore Database&#41; &#40;Analysis Services-dados multidimensionais&#41;](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Backup e restauração de bancos de dados do Analysis Services](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
