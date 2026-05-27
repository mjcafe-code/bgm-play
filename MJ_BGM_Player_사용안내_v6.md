# MJ Coffee Science — BGM 플레이어 사용 안내

작성: Hanrim (Cozy Shelter)

---

## 1. 개요

게시글별로 음악을 다르게 설정할 수 있는 **카페 스타일 BGM 플레이어**입니다.  
파일 하나(`bgm-player_cafe-ver.html`)로 모든 게시글에서 재사용하며, 음악·제목·이미지는 URL 파라미터로 전달합니다.

| 구분 | 내용 |
|---|---|
| **PC** | 캐릭터 이미지 + 곡 제목 + 재생/볼륨/시크바 + 접기/펼치기 버튼 |
| **모바일** | 플로팅 버튼(▶) → 클릭 시 하단 슬라이드 업 패널 표시 (이미지 + 제목 + 컨트롤) |

**디자인**: Playfair Display 세리프체 + 크림/브라운 카페 팔레트  
**skin.html 연동**: `mjcafe_skin_v4.html` 적용 시 재생 중 MJ Player v1.0 자동 정지

---

## 2. GitHub 파일 교체

`bgm-player_cafe-ver.html`을 `mjcafe-code/bgm-play` 저장소에 올려두시면 됩니다.

1. `mjcafe-code/bgm-play` 저장소 접속
2. `bgm-player_cafe-ver.html` 파일 업로드
3. 기존 `bgm-222.html`, `bgm-player.html`은 유지 권장 (기존 게시글 링크 호환)

---

## 3. 게시글에 적용하는 방법

게시글 본문에 아래 형식으로 iframe을 삽입하세요.

```html
<div class="music-player-box">
  <iframe
    src="https://mjcafe-code.github.io/bgm-play/bgm-player_cafe-ver.html?data=음악파일명|곡제목|이미지파일명"
    width="220" height="450" frameborder="0" scrolling="no">
  </iframe>
</div>
<script>
window.addEventListener('message', function(e) {
  if (e.data && e.data.type === 'bgm-resize') {
    document.querySelector('.music-player-box iframe').style.height = e.data.height + 'px';
  }
});
</script>
```

> `music-player-box`는 `mjcafe_skin_v4.html` 적용 시 자동으로 숨겨집니다.  
> skin.html의 카페 버전 플레이어가 해당 게시물에서 활성화됩니다.

### 파라미터 설명

`?data=` 뒤에 `|`(파이프)로 구분하여 순서대로 입력합니다.

| 순서 | 내용 | 필수 여부 |
|---|---|---|
| 1번째 | 음악 파일명 또는 URL | ✔ 필수 |
| 2번째 | 플레이어에 표시될 곡 제목 | 선택 (기본값: Background Music) |
| 3번째 | 이미지 파일명 또는 전체 URL | 선택 (기본값: violin-girl.png) |

> **곡 제목 줄바꿈**: ` / `(슬래시 앞뒤 공백)를 넣으면 두 줄로 표시됩니다.  
> 예: `The Swan / Yo-Yo Ma` → 두 줄로 표시

> ✔ **`|` 구분자 사용 이유**: 티스토리 에디터가 `&`를 `&amp;`로 자동 변환해 파라미터가 깨지는 문제를 방지하기 위한 방식입니다.

### 파일 입력 방식

**방식 1 — 저장소 파일명만 입력**  
`bgm-player_cafe-ver.html`과 같은 저장소에 파일이 있으면 파일명만 입력합니다.

```
?data=Vivaldi-Summer.m4a|Vivaldi / Summer|violin-girl.png
```

**방식 2 — 외부 전체 URL 입력 (권장)**  
티스토리 등 외부에 업로드한 파일의 전체 URL을 입력합니다.

```
?data=https://...음악파일.m4a|곡제목|https://...이미지파일.png
```

> 티스토리 이미지 URL은 **글쓰기 → 이미지 삽입 → 이미지 우클릭 → 이미지 주소 복사**로 얻을 수 있습니다.

---

## 4. 사용 예시

### 예시 1 — 비발디
```html
<div class="music-player-box">
  <iframe
    src="https://mjcafe-code.github.io/bgm-play/bgm-player_cafe-ver.html?data=Vivaldi-The_Four_Seasons_Summer_III_Presto.m4a|Vivaldi / Summer III Presto|violin-girl.png"
    width="220" height="450" frameborder="0" scrolling="no">
  </iframe>
</div>
```

### 예시 2 — 요요마 (The Swan)
```html
<div class="music-player-box">
  <iframe
    src="https://mjcafe-code.github.io/bgm-play/bgm-player_cafe-ver.html?data=Yo-Yo_Ma,Kathryn_Stott-The_Swan.m4a|The Swan / Yo-Yo Ma, Kathryn Stott|new_violin-girl.png"
    width="220" height="450" frameborder="0" scrolling="no">
  </iframe>
</div>
```

> 음악 파일과 이미지는 티스토리 **콘텐츠 → 파일 업로드**에서 업로드 후 링크 주소를 복사하여 사용하시면 됩니다.

> ⚠️ **모바일에서 직접 URL로 테스트하실 때 주의**  
> 곡 제목에 공백이 있는 경우 모바일 브라우저 주소창에 직접 입력 시 공백 위치에서 URL이 잘릴 수 있습니다.  
> 공백을 `%20`으로 바꿔서 입력해 주세요. 실제 게시글 iframe에서는 그대로 쓰셔도 됩니다.

---

## 5. 접기/펼치기

플레이어 우측 상단 `∨` / `∧` 버튼으로 접고 펼칠 수 있습니다.  
접힌 상태에서도 음악은 계속 재생됩니다.

---

## 6. skin.html 연동 (mjcafe_skin_v4.html 적용 시)

`mjcafe_skin_v4.html`을 적용하신 경우 두 플레이어가 자동으로 연동됩니다.

| 동작 | 결과 |
|---|---|
| 카페 버전 재생 | MJ Player v1.0 자동 정지 |
| MJ Player v1.0 재생 | 카페 버전 자동 정지 |

skin.html 적용 안내는 아래 Gist를 참고해 주세요.  
👉 https://gist.github.com/MerciHanrim/f6f5c2be8389c782923ef273c6c725a3

---

## 7. 기존 bgm-222.html 게시글 마이그레이션 (선택)

기존 게시글의 iframe src를 아래처럼 교체하시면 카페 버전으로 전환됩니다.

**변경 전**
```html
<iframe src="https://mjcafe-code.github.io/bgm-play/bgm-222.html" ...>
```

**변경 후**
```html
<iframe src="https://mjcafe-code.github.io/bgm-play/bgm-player_cafe-ver.html?data=Vivaldi-The_Four_Seasons_Summer_III_Presto.m4a|Vivaldi / Summer III Presto|violin-girl.png"
  width="220" height="450" frameborder="0" scrolling="no">
```

> 기존 파일은 그대로 두셔도 기존 게시글은 정상 동작합니다.  
> 새 게시글부터 `bgm-player_cafe-ver.html`을 사용하시면 됩니다.

---

## 8. 문의

적용 중 문제가 생기시거나 궁금한 점이 있으시면 편하게 말씀해 주세요 😊

- 이 페이지 하단 댓글창 (GitHub 계정으로 로그인 후 이용 가능)
- 블로그 댓글

편하신 방법으로 남겨주시면 됩니다!
