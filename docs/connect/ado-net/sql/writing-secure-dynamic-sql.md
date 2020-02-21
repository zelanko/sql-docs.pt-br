---
title: Gravação de SQL dinâmico seguro no SQL Server
description: Descreve técnicas para gravar SQL dinâmico seguro usando procedimentos armazenados.
ms.date: 09/26/2019
ms.assetid: df5512b0-c249-40d2-82f9-f9a2ce6665bc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 22d64b260d8d700afc8ed354d87de730e8c3b21f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75253369"
---
# <a name="writing-secure-dynamic-sql-in-sql-server"></a>Gravação de SQL dinâmico seguro no SQL Server

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

A injeção de SQL é o processo pelo qual um usuário mal-intencionado insere instruções Transact-SQL em vez de uma entrada válida. Se a entrada for passada diretamente para o servidor sem ser validada e se o aplicativo executar inadvertidamente o código injetado, o ataque terá o potencial de danificar ou destruir dados.  
  
Qualquer procedimento que construa instruções SQL deve ser verificado quanto a vulnerabilidades de injeção porque o SQL Server executará todas as consultas sintaticamente válidas que receber. Mesmo dados com parâmetros podem ser manipulados por um invasor qualificado e determinado. Se você usar SQL dinâmico, não deixe de parametrizar seus comandos e nunca inclua valores de parâmetro diretamente na cadeia de caracteres de consulta.  
  
## <a name="anatomy-of-a-sql-injection-attack"></a>Anatomia de um ataque de injeção de SQL  
O processo de injeção funciona encerrando prematuramente uma cadeia de caracteres de texto e anexando um novo comando. Como o comando inserido pode ter cadeias de caracteres adicionais anexadas a ele antes de ser executado, o malfeitor encerra a cadeia de caracteres injetada com uma marca de comentário "--". O texto subsequente é ignorado no momento da execução. Vários comandos podem ser inseridos usando um delimitador de ponto e vírgula (;).  
  
Contanto que o código SQL injetado esteja sintaticamente correto, a violação não poderá ser detectada programaticamente. Portanto, é necessário validar todas as entradas de usuário e verificar com cuidado o código que executa comandos SQL construídos no servidor que você está usando. Nunca concatene entrada de usuário que não seja validada. A concatenação de cadeia de caracteres é o ponto principal de entrada de injeção de script.  
  
Veja algumas diretrizes úteis:  
  
- Nunca compile instruções Transact-SQL diretamente da entrada do usuário; use procedimentos armazenados para validar a entrada do usuário.  
  
- Valide entrada de usuário testando tipo, comprimento, formato e intervalo. Use a função QUOTENAME() do Transact-SQL para escapar nomes do sistema ou a função REPLACE() para escapar qualquer caractere em uma cadeia de caracteres.  
  
- Implemente várias camadas de validação em cada nível do aplicativo.  
  
- Teste o tamanho e tipo de dados de entrada e imponha limites apropriados. Isso pode ajudar a impedir excesso deliberado de buffer.  
  
- Teste o conteúdo de variáveis de cadeia de caracteres e só aceite valores esperados. Rejeite entradas que contenham dados binários, sequências de escape e caracteres de comentário.  
  
- Quando você estiver trabalhando com documentos XML, valide todos os dados em seu esquema à medida que são inseridos.  
  
- Em ambientes de várias camadas, todos os dados devem ser validados antes de serem admitidos à zona confiável.  
  
- Não aceite as seguintes cadeias de caracteres nos campos dos quais os nomes de arquivo podem ser criados: AUX, CLOCK$, COM1 a COM8, CON, CONFIG$, LPT1 a LPT8, NUL e PRN.  
  
- Use objetos <xref:Microsoft.Data.SqlClient.SqlParameter> com procedimentos armazenados e comandos para fornecer verificação de tipo e validação de comprimento.  
  
- Use expressões <xref:System.Text.RegularExpressions.Regex> no código do cliente para filtrar caracteres inválidos.  
  
## <a name="dynamic-sql-strategies"></a>Estratégias dinâmicas de SQL  
A execução de instruções SQL criadas dinamicamente no seu código de procedimento quebra a cadeia de propriedade, fazendo com que SQL Server verifique as permissões do chamador em relação aos objetos que estão sendo acessados pelo SQL dinâmico.  
  
O SQL Server tem métodos para conceder aos usuários acesso a dados usando procedimentos armazenados e funções definidas pelo usuário que executam SQL dinâmico.  
  
- Usando a representação com a cláusula Transact-SQL EXECUTE AS.  
  
- Assinando procedimentos armazenados com um certificado.  
  
### <a name="execute-as"></a>EXECUTE AS  
A cláusula EXECUTE AS substitui as permissões do chamador com aquelas do usuário especificado na cláusula EXECUTE AS. Gatilhos ou procedimentos armazenados aninhados são executados sob o contexto de segurança do usuário proxy. Isso pode interromper os aplicativos que dependem da segurança em nível de linha ou que exigem auditoria. Algumas funções que retornam a identidade do usuário retornam o usuário especificado na cláusula EXECUTE AS, não o chamador original. O contexto de execução é revertido para o chamador original somente após a execução do procedimento ou quando uma instrução REVERT é emitida.  
  
### <a name="certificate-signing"></a>Assinatura de certificado  
Quando um procedimento armazenado que foi assinado com um certificado é executado, as permissões concedidas ao usuário do certificado são mescladas com as do chamador. O contexto de execução permanece o mesmo; o usuário do certificado não representa o chamador. A implementação da assinatura de procedimentos armazenados requer várias etapas. Cada vez que o procedimento é modificado, ele deve ser assinado novamente.  
  
### <a name="cross-database-access"></a>Acesso entre bancos de dados  
O encadeamento de propriedade entre bancos de dados não funciona nos casos em que instruções SQL criadas dinamicamente são executadas. Você pode solucionar isso no SQL Server criando um procedimento armazenado que acessa dados em outro banco de dados e assinando o procedimento armazenado com um certificado existente em ambos os bancos de dados. Isso dá aos usuários acesso aos recursos do banco de dados usados pelo procedimento, sem conceder a eles permissões nem acesso ao banco de dados.  
  
## <a name="external-resources"></a>Recursos externos  
Para obter mais informações, consulte os recursos a seguir.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|[Procedimentos armazenados](../../../relational-databases/stored-procedures/stored-procedures-database-engine.md) e [Injeção de SQL](../../../relational-databases/security/sql-injection.md) nos Manuais Online do SQL Server|Os tópicos descrevem como criar procedimentos armazenados e como a injeção de SQL funciona.|  
  
## <a name="next-steps"></a>Próximas etapas
- [Cenários de segurança de aplicativo no SQL Server](application-security-scenarios-sql-server.md)
