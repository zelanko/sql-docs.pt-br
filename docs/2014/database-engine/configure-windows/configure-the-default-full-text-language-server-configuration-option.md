---
title: Configurar a opção de configuração de servidor default full-text language | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- languages [full-text search]
- default full-text language option
ms.assetid: 0fa8785b-0830-4a52-aff5-fcf8268b72fc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d98194f5dead58b738c39503445923d9df49be06
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62787026"
---
# <a name="configure-the-default-full-text-language-server-configuration-option"></a>Configurar opção de configuração de servidor default full-text language
  Este tópico descreve como configurar a opção `default full-text language` de configuração de servidor [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o. A `default full-text language` opção especifica um valor de idioma padrão para índices de texto completo. A análise linguística é realizada em todos os dados que se encontram indexados com texto completo e depende do idioma dos dados. O valor padrão dessa opção é o idioma do servidor. Para uma versão localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a instalação define `default full-text language` a opção para o idioma do servidor se houver uma correspondência apropriada. Para uma versão não localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a opção `default full-text language` fica em inglês.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção default full-text language usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção default full-text language](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   O valor da `default full-text language` opção é usado em um índice de texto completo quando nenhum idioma é especificado para uma coluna por meio da opção Language **LANGUAGE_TERM** nas instruções CREATE FULLTEXT INDEX ou ALTER FULLTEXT index. Se o idioma de texto completo padrão não tiver suporte ou se o pacote de análise linguística não estiver disponível, a operação CREATE ou ALTER irá falhar e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará uma mensagem de erro informando que o idioma especificado não é válido.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou técnico certificado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   A `default full-text language` opção requer um valor LCID. Para ver uma lista de LCIDs com suporte e seus idiomas relacionados, consulte [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql). Outros idiomas também podem estar disponíveis; por exemplo, via fornecedores de software independentes. Se nenhum dialeto de idioma específico for encontrado, o serviço Mecanismo de Pesquisa de Texto Completo alternará para o idioma principal automaticamente.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-default-full-text-language-option"></a>Para configurar a opção default full-text language  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Avançado** .  
  
3.  Em Diversos, use **Idioma de Texto Completo Padrão** para especificar um valor de idioma padrão para colunas indexadas de texto completo.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-the-default-full-text-language-option"></a>Para configurar a opção default full-text language  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) para definir o valor da opção `default full-text` como Holandês (`1043`).  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'default full-text language', 1043 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
 Para obter mais informações, veja [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md).  
  
##  <a name="follow-up-after-you-configure-the-default-full-text-language-option"></a><a name="FollowUp"></a> Acompanhamento: depois de configurar a opção default full-text language  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
  
