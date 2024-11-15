<template>
  <header class="header">
    <!-- top nav -->
    <div class="top-nav" v-if="isLargeScreen"></div>
    <!-- Nav Bar -->
    <div class="navbar">
      <!-- hamber icon -->
      <div class="left-area" v-if="isNavbarVisible || isLargeScreen">
        <button class="menu-button" @click="toggleMenu">
          <span v-if="!isMenuOpen" class="hamber-icon"></span>
          <span v-if="!isMenuOpen" class="hamber-icon"></span>
          <span v-if="!isMenuOpen" class="hamber-icon"></span>
          <span v-else class="close-icon"></span>
        </button>

        <!-- logo -->
        <div class="logo">
          <img :src="logoSrc" width="100%" height="100%" alt="logo" />
        </div>
      </div>
      <!-- Search Bar - 寬螢幕：始終顯示 -->
      <div class="search-bar" v-if="isLargeScreen">
        <!-- 全部 -->
        <div class="category">
          <span class="category-label">全部</span>
          <span class="dropdown-icon">▼</span>
        </div>
        <!-- input -->
        <input type="text" class="search-input" placeholder="請輸入關鍵字" />
        <!-- 放大鏡 -->
        <button class="search-button">
          <span class="magnifier-icon">🔍</span>
        </button>
      </div>
      <!-- Search Bar 窄螢幕：滾動隱藏切換 -->
      <div
        class="search-bar"
        :class="{ expanded: isInputFocused }"
        v-if="!isLargeScreen && !isNavbarVisible"
      >
        <!-- 全部 -->
        <div class="category">
          <span class="category-label">全部</span>
          <span class="dropdown-icon">▼</span>
        </div>
        <!-- input -->
        <input
          type="text"
          class="search-input"
          :class="{ expanded: isInputFocused }"
          placeholder="請輸入關鍵字"
          @focus="handleFocus"
          @blur="handleBlur"
        />
        <!-- 放大鏡 -->
        <button class="search-button">
          <span class="magnifier-icon">🔍</span>
        </button>
      </div>
      <!-- 登入 -->
      <div class="right-area" v-if="isNavbarVisible || !isInputFocused">
        <!-- 會員限定 -->
        <div class="member-only" v-if="isLargeScreen">會員限定</div>
        <!-- Login -->
        <button class="login-button">登入</button>
        <button class="register-button" v-if="isLargeScreen">加入會員</button>
      </div>
    </div>

    <!-- Menu -->
    <div v-if="isMenuOpen" class="menu-overlay">
      <p>MENU</p>
    </div>
  </header>
</template>

<script>
import logoImage from "../assets/img/Logo.png";

export default {
  props: {
    isNavbarVisible: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      logoSrc: logoImage,
      isMenuOpen: false,
      isInputFocused: false,
      isLargeScreen: window.innerWidth >= 1440, // 初始判斷是否為寬螢幕
    };
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
    handleFocus() {
      this.isInputFocused = true;
    },
    handleBlur() {
      this.isInputFocused = false;
    },
    handleResize() {
      // 當螢幕尺寸改變時更新 isLargeScreen
      this.isLargeScreen = window.innerWidth >= 1440;
    },
  },
  mounted() {
    window.addEventListener("resize", this.handleResize);
  },
  beforeDestroy() {
    window.removeEventListener("resize", this.handleResize);
  },
};
</script>

<style scoped lang="scss">
@use "../assets/styles/variables.scss" as vars;

.header {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 30px;
  background-color: #fff;
  z-index: 2;

  @include vars.respond-to(large) {
    padding: 20px 0px;
    flex-direction: column;
  }
}

.top-nav {
  width: 100%;
  height: 32px;
  background-color: #b38e5b;
}

.navbar {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px;

  @include vars.respond-to(large) {
    width: 100%;
    padding: 20px;
    flex-grow: 1;
    // gap: 40px;
  }
}

.search-bar {
  display: flex;
  align-items: center;
  border: 1px solid #ccc;
  border-radius: 25px;
  padding: 5px;
  background-color: #fff;
  width: 235px;

  &.expanded {
    width: 339px;
  }

  @include vars.respond-to(large) {
    width: 400px;
    flex-grow: 1;
    max-width: 500px;
  }

  .category {
    display: flex;
    align-items: center;
    padding: 0 10px;
    border-right: 1px solid #ddd;
    width: 114px;

    @include vars.respond-to(large) {
      width: 150px;
    }
  }

  .category-label {
    font-size: 14px;
    color: #333;
  }

  .dropdown-icon {
    font-size: 12px;
    color: #333;
    margin-left: 5px;
  }

  .search-input {
    width: 121px;
    flex-grow: 1;
    border: none;
    padding: 5px;
    outline: none;
    transition: width 0.3s ease, padding 0.3s ease;
    font-size: 14px;
    background-color: #fff;
    color: #333;

    &::placeholder {
      color: #aaa;
    }

    &.expanded {
      width: 225px;
      padding: 5px 10px;
    }
    @include vars.respond-to(large) {
      width: 300px;
    }
  }

  .search-button {
    background: none;
    border: none;
    padding: 5px;
    cursor: pointer;
  }
}

.magnifier-icon {
  font-size: 20px;
  color: #aaa;
}

.left-area {
  display: flex;
  align-items: center;
  gap: 10px;
  @include vars.respond-to(large) {
    gap: 24px;
  }
}

.menu-button {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 3px;
  width: 24px;
  height: 24px;
  background: none;
  border: none;
  cursor: pointer;

  /* 三條橫線 */
  .hamber-icon {
    display: block;
    width: 100%;
    height: 2px;
    background-color: #000;
    border-radius: 1px;
    transition: all 0.3s ease;
  }

  .close-icon {
    position: relative;
    width: 100%;
    height: 100%;
  }

  /* X 圖示的樣式 */
  .close-icon::before,
  .close-icon::after {
    content: "";
    position: absolute;
    width: 100%;
    height: 2px;
    background-color: #000;
    top: 50%;
    left: 0;
    transform-origin: center;
    transition: all 0.3s ease;
  }

  /* 讓 X 圖示的兩條線交叉 */
  .close-icon::before {
    transform: translateY(-50%) rotate(45deg);
  }

  .close-icon::after {
    transform: translateY(-50%) rotate(-45deg);
  }
}

.menu-button:focus {
  outline: none;
}

.logo {
  width: 136px;
  height: 29px;
  background-color: white;
  color: #fff;

  @include vars.respond-to(large) {
    width: 150px;
  }
}

.right-area {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 10px;

  .login-button {
    width: 65px;
    height: 40px;
    color: #ff6700;
    border: 1px solid #ff6700;
    padding: 5px 10px;
    border-radius: 20px;
    background: none;
    cursor: pointer;

    &.hide {
      display: none;
    }
    @include vars.respond-to(large) {
      font-size: 16px;
    }
  }

  .register-button {
    width: 97px;
    height: 40px;
    color: #fff;
    border: none;
    border-radius: 20px;
    background: #ff6700;
  }
}

/* Menu overlay */
.menu-overlay {
  position: absolute;
  top: 100%;
  left: 0;
  width: 100%;
  height: 60vh;
  background-color: #f5f5f5;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 48px;
  color: #333;
  z-index: 1;

  @include vars.respond-to(large) {
    height: 80vh;
  }
}
</style>
