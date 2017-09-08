---
title: '@@OPTIONS (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 10/11/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@OPTIONS'
- '@@OPTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, current SET options
- '@@OPTIONS function'
- current SET options
ms.assetid: 3d5c7f6e-157b-4231-bbb4-4645a11078b3
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bc5a7b7899715ee06b8b0e6924893d0d8a04b14d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="options-transact-sql"></a>@@OPTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna informações sobre as opções SET atuais.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
@@OPTIONS  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **inteiro**  
  
## <a name="remarks"></a>Comentários  
 As opções podem vir do uso do **definido** comando ou o **opções de usuário de sp_configure** valor. Valores de sessão configurados com o **definir** comando substituir o **sp_configure** opções. Muitas ferramentas (tal como [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]) configuram automaticamente as opções do conjunto. Cada usuário tem uma @@OPTIONS função que representa a configuração.  
  
 Você pode alterar as opções de idioma e de processamento de consulta para uma sessão de usuário específico usando a instrução SET. **@@OPTIONS**  só pode detectar as opções que são definidas como ON ou OFF.  
  
 O **@@OPTIONS**  função retorna um bitmap das opções, convertidas em uma base 10 inteiro (decimal). As configurações de bits são armazenadas nas localizações descritas em uma tabela no tópico [configurar as opções de usuário a opção de configuração de servidor](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md).  
  
 Para decodificar o **@@OPTIONS**  valor, converta o inteiro retornado por **@@OPTIONS**  binário e, em seguida, examine os valores na tabela no [configurar as opções de usuário do servidor Opção de configuração](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md). Por exemplo, se `SELECT @@OPTIONS;` retorna o valor `5496`, use a Calculadora do programador do Windows (**calc.exe**) para converter decimal `5496` em binário. O resultado é `1010101111000`. Os caracteres mais à direita (binário 1, 2 e 4) são 0, indicando que os primeiros três itens na tabela são desativados. Consultando a tabela, verá que eles são **DISABLE_DEF_CNST_CHK** e **IMPLICIT_TRANSACTIONS**, e **CURSOR_CLOSE_ON_COMMIT**. O próximo item (**ANSI_WARNINGS** no `1000` posição) está em. Continuar trabalhando esquerda Embora o mapa de bits e para baixo na lista de opções. Quando as opções mais à esquerda são 0, elas serão truncadas pela conversão de tipo. O bitmap `1010101111000` é na verdade `001010101111000` para representar todas as 15 opções.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-demonstration-of-how-changes-affect-behavior"></a>A. Demonstração de como as alterações afetam o comportamento  
 O exemplo a seguir demonstra a diferença no comportamento de concatenação com duas configurações diferentes do **CONCAT_NULL_YIELDS_NULL** opção.  
  
```  
SELECT @@OPTIONS AS OriginalOptionsValue;  
SET CONCAT_NULL_YIELDS_NULL OFF;  
SELECT 'abc' + NULL AS ResultWhen_OFF, @@OPTIONS AS OptionsValueWhen_OFF;  
  
SET CONCAT_NULL_YIELDS_NULL ON;  
SELECT 'abc' + NULL AS ResultWhen_ON, @@OPTIONS AS OptionsValueWhen_ON;  
```  
  
### <a name="b-testing-a-client-nocount-setting"></a>B. Testando uma configuração de cliente NOCOUNT  
 O exemplo a seguir define `NOCOUNT``ON` e, em seguida, testa o valor de `@@OPTIONS`. O `NOCOUNT``ON` opção impede que a mensagem sobre o número de linhas afetadas seja enviada para o cliente solicitante para cada instrução em uma sessão. O valor de `@@OPTIONS` é definido como `512` (0x0200). Isto representa a opção NOCOUNT. Este exemplo testa se a opção NOCOUNT está habilitada no cliente. Por exemplo, isso pode ajudar a controlar diferenças de desempenho em um cliente.  
  
```  
SET NOCOUNT ON  
IF @@OPTIONS & 512 > 0   
RAISERROR ('Current user has SET NOCOUNT turned on.', 1, 1)  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de configuração &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Configurar as opções de configuração do servidor user options](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)  
  
  

