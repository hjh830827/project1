<template>
  <div v-show="deliveryMethodSelectedFlag && selectedMethod !== ''" class="buyer-info">
    <div class="buyer-tit">
      <h3 class="tit">배송정보</h3>
      <a v-show="firstUserAddressFlag" href="#none" class="notice" @click.prevent="modifyAddress(true)">
        이 주소가 아닌가요?
      </a>
      <a
        v-show="!firstUserAddressFlag && formConfirmedFlag"
        href="#none"
        class="notice"
        @click.prevent="modifyAddress()"
        >수정</a
      >
    </div>
    <!-- 입력된 텍스트 -->
    <ul v-show="firstUserAddressFlag" class="buyer-list">
      <li class="buyer-item">
        <span for="_deliveryParcelPhone2" class="title">휴대폰 번호</span>
        <div class="form-group">
          <span class="c-input"> 010-1234-5678 </span>
        </div>
      </li>
      <li class="buyer-item">
        <strong class="title">주소</strong>
        <div class="detail-address">
          <div class="form-group">
            <span class="c-input">
              <span>15950</span>
              <span>서울시 중구 을지로(을지로 1가)</span>
              <span>페럼타워 14층</span>
            </span>
          </div>
        </div>
      </li>
    </ul>
    <!-- //입력된 텍스트 -->

    <!-- 입력된 텍스트 -->
    <ul v-show="!firstUserAddressFlag && formConfirmedFlag" class="buyer-list">
      <li class="buyer-item">
        <span for="_deliveryParcelPhone2" class="title">휴대폰 번호</span>
        <div class="form-group">
          <span class="c-input"> 010-1234-5678 </span>
        </div>
      </li>
      <li class="buyer-item">
        <strong class="title">주소</strong>
        <div class="detail-address">
          <div class="form-group">
            <span class="c-input">
              <span>15950</span>
              <span>서울시 중구 을지로(을지로 1가)</span>
              <span>페럼타워 14층</span>
            </span>
          </div>
        </div>
      </li>
    </ul>
    <!-- //입력된 텍스트 -->

    <!-- 입력 폼 -->
    <div v-show="!firstUserAddressFlag && !formConfirmedFlag">
      <ul class="buyer-list">
        <li class="buyer-item">
          <label for="_deliveryParcelPhone2" class="title">휴대폰 번호</label>
          <div class="form-group">
            <span class="c-input">
              <input
                id="_deliveryParcelPhone2"
                type="tel"
                placeholder="- 없이 숫자만 입력해주세요"
                class="input"
                required=""
                maxlength="11"
                value="010-1234-5678"
                readonly="readonly"
              />
            </span>
          </div>
        </li>
        <li class="buyer-item">
          <strong class="title">주소</strong>
          <div class="detail-address">
            <div class="form-group">
              <span class="c-input">
                <input
                  type="number"
                  title="우편번호"
                  class="input"
                  value="12345"
                  readonly="readonly"
                  required=""
                  pattern="[0-9]*"
                  inputmode="numeric"
                />
              </span>
              <button type="button" class="btn-extra" @click="openPopupZipcode">우편번호 찾기</button>
            </div>
            <div class="form-group">
              <span class="c-input">
                <input
                  type="text"
                  title="기본 주소"
                  value="경기도 광주시 오포읍 신현리"
                  class="input"
                  readonly="readonly"
                  required=""
                />
              </span>
            </div>
            <div class="form-group">
              <span class="c-input">
                <input
                  type="text"
                  title="나머지 주소"
                  value="638-3 주원타운 102동 403호"
                  maxlength="50"
                  class="input"
                  readonly="readonly"
                />
              </span>
            </div>
          </div>
        </li>
      </ul>
      <button type="button" class="btn-submit" @click.prevent="ConfirmInputForm">확인</button>
    </div>
    <!-- //입력 폼 -->
  </div>
</template>

<script>
export default {
  components: {},
  props: {
    selectedMethod: {
      type: String,
      required: true,
      default: ''
    },
    deliveryMethodSelectedFlag: {
      type: Boolean,
      required: true,
      default: true
    },
    userInfoExistFlag: {
      type: Boolean,
      required: true,
      default: false
    }
  },
  data() {
    return {
      // 처음 받아온 사용자 주소 flag
      firstUserAddressFlag: false,

      // 사용자 주소 입력폼 완료 flag
      formConfirmedFlag: false,

      // 사용자 전화번호
      userPhoneNumber: ''
    };
  },
  watch: {},
  created() {
    this.firstUserAddressFlag = this.userInfoExistFlag;
  },
  mounted() {},
  methods: {
    /**
     * 사용자 주소를 수정한다.
     * @function
     * @param {boolean} firstFlag - 처음 받아온 사용자 주소를 수정할 때 true 입력. 그 외에는 값을 입력하지 않는다.
     */
    modifyAddress(firstFlag) {
      this.formConfirmedFlag = false;

      // 처음 받아온 사용자 주소가 있을 때 수정을 진행하려고 한 뒤에는, 일반 수정/입력 상태로 바뀐다.
      if (firstFlag) this.firstUserAddressFlag = false;
    },

    /**
     * 입력하거나 수정한 내용을 확정한다.
     * @function
     */
    ConfirmInputForm() {
      this.formConfirmedFlag = true;
    },

    /**
     * 주소 검색 팝업을 보인다.
     * @function
     */
    openPopupZipcode() {
      this.$emit('openPopupZipcode');
    }
  }
};
</script>

<style lang="scss" scoped></style>
