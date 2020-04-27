---
title: Caixa de diálogo backup Database (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.Backup.f1
ms.assetid: 7811ce7d-6c37-4189-bfa6-ef36fb4932db
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a99ce67c4b42cc1def10127c8b1862a859d20723
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66064376"
---
# <a name="backup-database-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Banco de Dados de Backup (Analysis Services - Dados multidimensionais)
  Use a caixa de diálogo **Banco de Dados de Backup** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para fazer backup de um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] em um arquivo de backup usando o formato Analysis Services Backup File (.abf) do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  Para cada arquivo de backup, o usuário que executar o comando de backup deve ter permissão para gravar no local de backup especificado de cada arquivo. Além disso, o usuário deve ter uma das seguintes funções: membro de uma função de servidor para a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou membro de uma função de banco de dados com permissões de Controle total (Administrador) no banco de dados cujo backup será feito.  
  
 **Para exibir a caixa de diálogo Banco de Dados de Backup**  
  
-   No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], clique com o botão direito do mouse na pasta **Bancos de Dados** de uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou em um banco de dados no **Pesquisador de Objetos**e então clique em **Backup**.  
  
## <a name="options"></a>Opções  
 **Script**  
 Cria um script de backup baseado nas opções selecionadas na caixa de diálogo. O script de restauração é escrito na Linguagem de Scripts do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] (ASSL).  
  
 Clicar no ícone **Script** envia o script de backup a uma nova janela de consulta, por padrão.  
  
 Clicar na seta **Script** exibe um menu que permite escolher para onde enviar o script de backup:  
  
-   Para uma nova janela de consulta (padrão).  
  
-   Para um arquivo.  
  
-   Para a área de transferência.  
  
-   Para um trabalho.  
  
 **Backup de banco de dados**  
 Exibe o nome do banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] atualmente selecionado.  
  
 **Arquivo de backup**  
 Digite o caminho completo e nome do arquivo de backup a utilizar.  
  
 **Procurar**  
 Clique para exibir a caixa de diálogo **Salvar Arquivo Como** e selecionar o caminho e nome do arquivo de backup a utilizar. Para obter mais informações sobre a caixa de diálogo **Salvar Arquivo Como**, consulte [Caixa de diálogo Salvar Arquivo Como &#40;Analysis Services – Dados Multidimensionais&#41;](save-file-as-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Permitir substituição de arquivos**  
 Selecione para substituir um arquivo de backup existente ou arquivo de backup remoto, se houver um.  
  
> [!NOTE]  
>   Se esta opção não for selecionada e existir o arquivo de backup especificado em **Arquivo de backup** ou um arquivo de backup remoto especificado em **Arquivo de backup remoto** , ocorre um erro.  
  
 **Aplicar compactação**  
 Selecione para compactar os conteúdos do arquivo de backup e, se especificado, dos arquivos de backup remotos.  
  
 **Criptografar arquivo de backup**  
 Selecione para criptografar o arquivo de backup usando a senha fornecida em **Senha**.  
  
 **Senha**  
 Digite a senha a ser usada ao criptografar o arquivo de backup e, se especificados, arquivos de backup remotos.  
  
> [!NOTE]  
>   Esta opção só será habilitada se **Criptografar arquivo de backup** for selecionado.  
  
 **Confirmar Senha**  
 Digite a senha que foi utilizada em **Senha** para confirmar a senha para o arquivo de backup e, se especificados, arquivos de backup remotos.  
  
> [!NOTE]  
>   Esta opção só será habilitada se **Criptografar arquivo de backup** for selecionado.  
  
 **Fazer backup de partição(ões) remota(s)**  
 Selecione para incluir informações de local e dados para partições remotas no arquivo de backup.  
  
> [!NOTE]  
>  Esta opção só será habilitada se o banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] atualmente selecionado usar partições remotas.  
  
 **Local de backup da partição remota**  
 Exibe o local das partições remotas associadas com o banco de dados selecionado, como também o arquivo de backup remoto usado para fazer backup de dados e metadados para as partições remotas. As seguintes colunas estão disponíveis:  
  
|Coluna|Descrição|  
|------------|-----------------|  
|**Servidor**|Exibe a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que administra as partições remotas.|  
|**Backup de banco de dados**|Exibe o banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que contém as partições remotas.|  
|**Lista de Partições**|Exibe a lista de partições remotas contidas no banco de dados exibido em **Banco de Dados**.|  
|**Arquivo de backup remoto**|Digite o caminho completo e o nome de arquivo do arquivo de backup remoto a ser usado, ou clique no botão de reticências (**...**) para exibir a caixa de diálogo **Salvar Arquivo Como** e selecionar o caminho e o nome de arquivo do arquivo de backup remoto a ser usado. Para obter mais informações sobre a caixa de diálogo **Salvar Arquivo Como**, consulte [Caixa de diálogo Salvar Arquivo Como &#40;Analysis Services – Dados Multidimensionais&#41;](save-file-as-dialog-box-analysis-services-multidimensional-data.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Analysis Services designers e caixas de diálogo &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Backup e restauração de bancos de dados do Analysis Services](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
