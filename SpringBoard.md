# Spring

>게시판 만들기 소스 분석
- - -
## A.4서비스 구현

### BoardService.java

#### repo : com.heaven.mva.board.service
```
package com.heaven.mvc.board.service;

import java.util.List;
import com.heaven.mvc.board.domain.BoardVO;

public interface BoardService {
	
	public abstract List<BoardVO> list();
	
	public abstract int delete(BoardVO boardVO);
	
	public abstract int edit(BoardVO boardVO);
	
	public abstract void write(BoardVO boardVO);
	
	public abstract BoardVO read(int seq);

}

```

### BoardServiceImpl.java

#### repo : com.heaven.mva.board.service
```
package com.heaven.mvc.board.service;

import java.util.List;

import javax.annotation.Resource;

import org.springframework.stereotype.Service;

import com.heaven.mvc.board.dao.BoardDao;
import com.heaven.mvc.board.domain.BoardVO;

@Service
public class BoardServiceImpl implements BoardService {
	@Resource
	private BoardDao boardDao;
	
	public BoardDao getBoardDao() {
		return boardDao;
	}

	public void setBoardDao(BoardDao boardDao) {
		this.boardDao = boardDao;
	}
	
	@Override
	public List<BoardVO> list() {
		return boardDao.list();
	}
	
	@Override
	public int delete(BoardVO boardVO) {
		return boardDao.delete(boardVO);
	}
	
	@Override
	public int edit(BoardVO boardVO) {
		return boardDao.update(boardVO);
	}
	
	@Override
	public void write(BoardVO boardVO) {
		boardDao.insert(boardVO);
	}
	
	@Override
	public BoardVO read(int seq) {
		boardDao.updateReadCount(seq);
		return boardDao.select(seq);
	}
}

```
