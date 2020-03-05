# RESTful

Segundo Roy Fielding  
> *Uma aplicação web (...) é uma rede de **recursos** web (uma máquina de estado virtual) onde o usuário progride ao longo da aplicação por meio de links (que são URIs), como /user/tom, e operações como GET ou DELETE (transições de estado), resultando no próximo recurso (representando o próximo estado da aplicação) sendo transferido ao usuário para sua utilização.*

Quando uma aplicação segue o estilo arquitetural REST dizemos que ela é RESTful.

E quando a aplicação é RESTful ela expõe recursos e subrecursos, que são identificados por meio de URIs:
```
GET /Livros/{id}            //expondo um recurso
GET /Livros/{id}/capa       //expondo um subrecurso
```

**Boas práticas e algumas constraints/restrições para ser RESTful:**

- Retorne o código de status que traz semântica para o ocorrido.
- Use o verbo http adequado e não post para tudo.
- Não está errado usar o singular. O importante é padronizar, ou seja, vai usar plural ou singular.
- Evite usar verbos no nome do método. Use substantivos, pois o verbo deve ser no método http que por sua vez aponta para um recurso/substantivo.
- Não deixe uma barra no final.
- Stateless: a request deve ter tudo o que é necessário para o server entender e retornar a response. A sessão do usuário não pode ser armazenada no server, ela deve ser enviada em todas as requisições. Podemos fazer isso por meio de tokens.
- Cacheable: o server deve retornar se a resposta pode ou não ser cacheada no cliente.
- Layered System: o cliente não precisa saber quantas camadas foram necessárias para resolver a requisição.
- 

**DotNet:**

```c#
[HttpGet] ou [HttpGet("{id}")] ou [HttpGet("Xpto/{id}")]
[HttpPost]
[HttpPut]
[HttpDelete("{id}")]
public IActionResult<algo> Metodo(...)
{
	return OK(<algo>);				//200 - ok
	return Created(uri, model);		//201 - o recurso foi criado com sucesso
	return NoContent();				//204 - ok, o recurso foi removido com sucesso
	return BadRequest(); 			//400 - requisição inválida ou erro na requisição
	return NotFound();				//404 - o recurso solicitado não existe
}
```

**Grupos de Status de Resposta:**

- **1xx**: Informações
- **2xx**: Sucesso
- **3xx**: Redirecionamento
- **4xx**: Erro originado pelo cliente - o cliente solicitou algo que não existe ou enviou uma solicitação inválida. Nestes casos o cliente precisa rever sua requisição ou entender melhor como enviar a requisição.
- **5xx**: Erro originado pelo servidor - em tese o cliente fez tudo certo, mas ocorreu algum erro inesperado no servidor. Neste caso o fornecedor da API precisa tratar o problema.

---

**Referências:**

* https://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html
* https://docs.microsoft.com/pt-br/aspnet/core/web-api/action-return-types
* https://www.talkingdotnet.com/return-http-status-code-from-asp-net-core-methods
* https://martinfowler.com/articles/richardsonMaturityModel.html
* https://medium.com/@osaigbovoemmanuel1/is-the-richardson-maturity-model-relevant-in-2019-80e0cd211483
* https://www.youtube.com/watch?v=r62JVRAeqyk (curso)