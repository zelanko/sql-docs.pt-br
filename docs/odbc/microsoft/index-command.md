---
title: Comando INDEX | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- index command [ODBC]
ms.assetid: 694e8cf5-2f69-4001-9c1e-b735a4da3aff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bcb30a49cb9f11ddd4c61621116aa4bd8ddcf186
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300026"
---
# <a name="index-command"></a>Comando INDEX
Cria um arquivo de índice para exibir e acessar registros de tabela em uma ordem lógica.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
INDEX ON eExpression TO IDXFileName | TAG TagName [OF CDXFileName]  
   [FOR lExpression]  
   [COMPACT]  
   [ASCENDING | DESCENDING]  
   [UNIQUE | CANDIDATE]  
   [ADDITIVE]  
```  
  
## <a name="arguments"></a>Argumentos  
 *eExpression*  
 Especifica uma expressão de índice que pode incluir o nome de um campo ou campos da tabela atual. Uma chave de índice com base na expressão do índice é criada no arquivo de índice para cada registro na tabela. Visual FoxPro usa essas teclas para exibir e acessar registros na tabela.  
  
> [!NOTE]  
>  Embora não seja recomendado, *o eExpression* também pode ser uma variável de memória, um elemento de array ou uma expressão de campo ou campo de uma tabela em outra área de trabalho. Os campos de memorando não podem ser usados sozinhos em expressões de arquivo de índice; eles devem ser combinados com outras expressões de caráter. Se você acessar um índice que contenha uma variável ou campo que não existe ou não pode ser localizado, o Visual FoxPro gerará uma mensagem de erro.  
  
 Se você tentar construir um índice com uma chave que varia de comprimento, a chave será acolchoada com espaços. As teclas de índice de comprimento variável não são suportadas no Visual FoxPro.  
  
 É possível criar uma chave de índice com comprimento zero. Por exemplo, uma chave de índice de comprimento zero é criada quando a expressão do índice é uma substring de um campo de memorando vazio. Uma chave de índice de comprimento zero gera uma mensagem de erro. Quando o Visual FoxPro cria um índice, ele avalia os campos no primeiro registro na tabela. Se um campo estiver vazio, pode ser necessário inserir alguns dados temporários no campo no primeiro registro para evitar uma chave de índice de 0 comprimento.  
  
 Para *IDXNome de arquivo*  
 Cria um arquivo de índice .idx. O arquivo de índice recebe a extensão padrão .idx.  
  
 TagNome *[DE* *CDXFileName*]  
 Cria um arquivo de índice composto. Um arquivo de índice composto é um arquivo de índice único que consiste em qualquer número de tags separadas (entradas de índice). Cada tag é identificada pelo nome da tag única. Os nomes das marcas devem começar com uma letra ou um sublinhado e podem consistir em qualquer combinação de até 10 letras, dígitos ou sublinhados. O número de tags em um arquivo de índice composto é limitado apenas pela memória disponível e espaço em disco.  
  
 Os arquivos de índice composto de entrada múltipla são sempre compactos. Não é necessário incluir COMPACT ao criar um arquivo de índice composto. Os nomes dos arquivos de índice composto recebem uma extensão .cdx.  
  
 Dois tipos de arquivos de índice composto podem ser criados: estrutural e não estrutural.  
  
 **Arquivos de índice composto estrutural** Você pode criar um arquivo de índice composto estrutural com *TAGName,* excluindo a cláusula opcional *de CDXFileName.* Um arquivo de índice composto estrutural sempre tem o mesmo nome de base da tabela e é automaticamente aberto quando a tabela é aberta.  
  
 **Arquivos de índice composto não estrutural** Você pode criar um arquivo de índice composto não estrutural incluindo *cdxfilename* após *TAGName*. Ao contrário de um arquivo de índice composto estrutural, um arquivo de índice composto não estrutural deve ser explicitamente aberto com a cláusula INDEX em USO.  
  
 Se um arquivo de índice composto já tiver sido criado e aberto, a emissão de ÍNDICE com *TAGName taga* adicionar uma tag ao arquivo de índice composto.  
  
 PARA *lExpression*  
 Especifica uma condição pela qual apenas registros que satisfaçam a expressão do filtro *lExpression* estão disponíveis para exibição e acesso; as teclas de índice são criadas no arquivo de índice para apenas aqueles registros que correspondem à expressão do filtro.  
  
 A tecnologia Visual FoxPro Rushmore otimiza um ÍNDICE ... Para o comando *lExpression* se *lExpression* for uma expressão otimizada. Para obter o melhor desempenho, use uma expressão otimizada na cláusula FOR.  
  
 Compacto  
 Cria um arquivo compact .idx.  
  
 Crescente  
 Especifica uma ordem ascendente para o arquivo .cdx. Por padrão, as tags .cdx são criadas em ordem crescente. (Você pode incluir ASCENDING como um lembrete da ordem do arquivo de índice.) Uma tabela pode ser indexada em ordem inversa, incluindo DESCENDING.  
  
 Descendente  
 Especifica uma ordem decrescente para o arquivo .cdx. Você não pode incluir DESCENDING ao criar arquivos de índice .idx.  
  
 UNIQUE  
 Especifica que apenas o primeiro registro encontrado com um determinado valor de chave de índice está incluído em um arquivo .idx ou uma tag .cdx. O UNIQUE pode ser usado para impedir a exibição ou o acesso a registros duplicados. Todos os registros adicionados com chaves de índice duplicadas são excluídos do arquivo de índice. O uso da opção UNIQUE do INDEX é idêntico ao executar SET UNIQUE ON antes de emitir INDEX ou REINDEX.  
  
 Quando uma tag de índice OU índice UNIQUE está ativa e um registro duplicado é alterado de uma maneira que altera sua tecla de índice, a tag índice ou índice é atualizada. No entanto, o próximo registro duplicado com a chave de índice original não pode ser acessado ou exibido até que você reindexe o arquivo usando REINDEX.  
  
 Candidato  
 Cria uma etiqueta de índice estrutural do candidato. A palavra-chave CANDIDATE só pode ser incluída ao criar uma tag de índice estrutural; caso contrário, o Visual FoxPro gera uma mensagem de erro.  
  
 Uma tag de índice do candidato impede valores duplicados no campo ou combinação de campos especificados na expressão de índice *eExpression*. O *termo candidato* refere-se ao tipo de índice; porque os índices dos candidatos impedem valores duplicados, eles se qualificam como um "candidato" para ser um índice primário.  
  
 Visual FoxPro gera um erro se você criar uma tag de índice de candidato para um campo ou combinação de campos que já contenham valores duplicados.  
  
 Aditivo  
 Mantém aberto qualquer arquivo de índice aberto anteriormente. Se você omite a cláusula ADITIVA ao criar um arquivo de índice ou arquivos para uma tabela com INDEX, quaisquer arquivos de índice abertos anteriormente (exceto o índice composto estrutural) serão fechados.  
  
## <a name="remarks"></a>Comentários  
 Os registros em uma tabela que tenha um arquivo de índice são exibidos e acessados na ordem especificada pela expressão do índice. A ordem física dos registros na tabela não é alterada por um arquivo de índice.  
  
## <a name="index-types"></a>Tipos de Índice  
 O Visual FoxPro permite criar dois tipos de arquivos de índice:  
  
-   Arquivos de índice composto .cdx contendo várias entradas de índice chamadas tags  
  
-   Arquivos de índice .idx contendo uma entrada de índice  
  
 Você também pode criar um arquivo de índice composto estrutural, que é aberto automaticamente com a tabela.  
  
> [!NOTE]  
>  Como os arquivos de índice composto estrutural são abertos automaticamente quando a tabela é aberta, eles são o tipo de índice preferido.  
  
 Inclua COMPACT para criar arquivos de índice .idx compactos. Os arquivos de índice composto são sempre compactos.  
  
## <a name="index-order-and-updating"></a>Ordem e Atualização de Índice  
 Apenas um arquivo de índice (o arquivo de índice mestre) ou tag (a tag mestre) controla a ordem na qual a tabela é exibida ou acessada. Certos comandos (SEEK, por exemplo) usam o arquivo de índice mestre ou tag para procurar registros. No entanto, todos os arquivos de índice .idx e .cdx abertos são atualizados à medida que as alterações são feitas na tabela.  
  
## <a name="user-defined-functions"></a>Funções definidas pelo usuário  
 Embora uma expressão de índice possa conter uma função definida pelo usuário, você não deve usar funções definidas pelo usuário em uma expressão de índice. Funções definidas pelo usuário em uma expressão de índice aumentam o tempo necessário para criar ou atualizar o índice. Além disso, as atualizações de índice podem não ocorrer quando uma função definida pelo usuário é usada para uma expressão de índice.  
  
 Se você usar uma função definida pelo usuário em uma expressão de índice, o Visual FoxPro deve ser capaz de localizar a função definida pelo usuário. Quando o Visual FoxPro cria um índice, a expressão do índice é salva no arquivo de índice, mas apenas uma referência à função definida pelo usuário é incluída na expressão do índice.  
  
## <a name="see-also"></a>Consulte Também  
 [TABELA ALTER - Comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Comando DELETE TAG](../../odbc/microsoft/delete-tag-command.md)   
 [DEFINIR Comando COLLATE](../../odbc/microsoft/set-collate-command.md)   
 [Comando SET UNIQUE](../../odbc/microsoft/set-unique-command.md)
